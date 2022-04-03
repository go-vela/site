---
title: "Kubernetes"
linkTitle: "Kubernetes"
weight: 3
description: >
  This section contains information on deploying the Vela worker service with Kubernetes.
---

## Prerequisites

This section provides all required dependencies to install and start the worker with Kubernetes.

### Dependency 1: Kubernetes

[Kubernetes](https://kubernetes.io/) will be used for downloading the worker and managing the lifecycle of the application.

You can refer to [Kubernetes' official documentation](https://kubernetes.io/docs/setup/) on installing and configuring the service.

### Dependency 2: Redis

[Redis](https://redis.io/) will be used for storing workloads, created by the [server](/docs/administration/server/), that will be run by a worker.

You can refer to [Redis's official documentation](https://redis.io/topics/quickstart/) on installing and configuring the service.

## Installation

This section provides an example of installing the worker with Kubernetes.

This example only shows a subset of all possible configuration options.

### Step 1: Create a Worker Secret and ConfigMap

You will need to store some env vars in a `Secret`, and the rest can go in a `ConfigMap`.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: vela-worker
  namespace: default
data:
  # these values are base64 encoded

  VELA_SERVER_SECRET: PHNoYXJlZC1zZWNyZXQ+
  # VELA_SERVER_SECRET: <shared-secret>

  VELA_QUEUE_ADDR: cmVkaXM6Ly88cGFzc3dvcmQ+QDxob3N0bmFtZT46PHBvcnQ+LzxkYXRhYmFzZT4=
  # VELA_QUEUE_ADDR: redis://<password>@<hostname>:<port>/<database>
```

Do not store any passwords in the `ConfigMap`. The `ConfigMap` is more convenient for everything else.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: vela-worker
  namespace: default
data:
  # This might be "http://vela-server:8080" if vela-server is also deployed in k8s.
  VELA_SERVER_ADDR: https://vela-server.example.com

  VELA_QUEUE_DRIVER: redis

  VELA_EXECUTOR_DRIVER: linux

  VELA_RUNTIME_DRIVER: kubernetes
  VELA_RUNTIME_NAMESPACE: default
  VELA_RUNTIME_PODS_TEMPLATE_NAME: pipeline-pods-template

  # do not define VELA_WORKER_ADDR here. See "Create a Worker Deployment" below.

  # VELA_RUNTIME_CONFIG is not needed in-cluster.
  # We'll use the auto-mounted ServiceAccount Token.
```

And then load them in your cluster.

```shell
$ kubectl apply -f worker-secret.yaml
$ kubectl apply -f worker-configmap.yaml
```

{{% alert title="Note:" color="primary" %}}
For a full list of configuration options, please see the [worker reference](/docs/administration/worker/reference/).
{{% /alert %}}


### Step 2: Load the Pipeline Pods Template CRD

Download Vela's "Pipeline Pods Template" Custom Resource Definition (CRD).
Be sure to replace `v0.14.0` with the version you're installing.

```shell
$ curl https://raw.githubusercontent.com/go-vela/worker/v0.14.0/runtime/kubernetes/generated/go-vela.github.io_pipelinepodstemplates.yaml -o go-vela.github.io_pipelinepodstemplates.yaml
```

And then add the CRD to your cluster.

```shell
$ kubectl apply -f go-vela.github.io_pipelinepodstemplates.yaml
```

### Step 3: Create a Pipeline Pods Template

The Pipeline Pods Template allows you to define `annotations`, `securityContext`, `dnsConfig`
and other settings that the worker should add to every Pipeline's `Pod`.

```yaml
apiVersion: go-vela.github.io/v1alpha1
kind: PipelinePodsTemplate
metadata:
  name: pipeline-pods-template # this should match VELA_RUNTIME_PODS_TEMPLATE_NAME
  namespace: default
spec:
  # spec.template is a subset of what is possible to define in a Deployment's "spec.template".
  template:

    metadata:
      # custom annotations to add to all pipeline pods
      annotations:
        example.com/owner: devops
      #labels:

    #spec:
    #  dnsConfig: {}
    #  dnsPolicy: ClusterFirst

    #  nodeSelector: {}
    #  tolerations: []
    #  affinity: {}

    #  # These gets applied to all containers in the Pipeline Pod.
    #  container:
    #    securityContext:
    #      capabilities:
    #        drop: ["ALL"]
    #        add: []
```

And then your `PipelinePodsTemplate` to your cluster.

```shell
$ kubectl apply -f pipeline-pods-template.yaml
```

### Step 5: Create a ServiceAccount, Role, and RoleBinding

The Worker needs access to Kubernetes APIs. It uses an auto-mounted ServiceAcount token to do this.

Here is a ServiceAccount:
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: vela-worker
  namespace: default
```

Here's the Role you'll need:
```yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: vela-worker
  namespace: default
rules:
  - apiGroups: [""]
    resources: [pods/log]
    verbs: [get, list, watch]
  - apiGroups: [""]
    resources: [pods]
    verbs: [create, patch, get, list, update, watch, delete]
  - apiGroups: ["go-vela.github.io"]
    resources: [pipelinepodstemplate]
    verbs: [get, list, watch]
```

And use this RoleBinding:
```yaml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: vela-worker
  namespace: default
subjects:
  - kind: ServiceAccount
    name: vela-worker
    namespace: default
roleRef:
  kind: Role
  name: vela-worker
  apiGroup: rbac.authorization.k8s.io
```

Then apply each of these to your cluster:

```shell
$ kubectl apply -f worker-serviceaccount.yaml
$ kubectl apply -f worker-role.yaml
$ kubectl apply -f worker-role-binding.yaml
```

### Step 5: Create a Worker Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: vela-worker
  namespace: default
  labels:
    app.kubernetes.io/name: vela-worker
spec:
  replicas: 1 # Increase this to deploy more worker pods.
  selector:
    matchLabels:
      app.kubernetes.io/name: vela-worker
  serviceAccount: vela-worker
  containers:
    - name: worker
      image: target/vela-worker:v0.13.0
      ports:
        - {name: http, port: 8080, protocol: TCP}
      livenessProbe:
        httpGet: {path: /health, port: 8080, scheme: HTTP}
      env:
        - {name: VELA_WORKER_ADDR_SCHEME, value: http}
        - {name: VELA_WORKER_ADDR_PORT, value: "8080"}
        - name: VELA_WORKER_POD_NAME
          valueFrom:
            fieldRef: {fieldPath: metadata.name}
        - name: VELA_WORKER_POD_IP
          valueFrom:
            fieldRef: {fieldPath: status.podIP}
        # using the pod name does not get a dns entry without a lot of unnecessary effort.
        # So, here we use status.podIP instead of metadata.name
        - name: VELA_WORKER_ADDR
          value: $(VELA_WORKER_ADDR_SCHEME)://$(WORKER_POD_IP):$(VELA_WORKER_ADDR_PORT)
      envFrom:
        - configMapRef:
            name: vela-worker
        - secretRef:
            name: vela-worker
```

And then load it in your cluster.

```shell
$ kubectl apply -f worker-deployment.yaml
```

### Step 6: Verify the Worker Deployment

Ensure the worker started up successfully and is running as expected by inspecting details with `kubectl`.

```shell
$ kubectl describe deployment vela-worker
$ kubectl get pods -l app.kubernetes.io/name=vela-worker
```

You can also check the worker logs with `stern`. The following command will tail all of the logs
for pods that start with `vela-worker-`:

```shell
$ stern vela-worker-
```