---
title: "Pipe"
weight: 10
description: >
  Learn how to generate a pipeline file.
---

## Information

The generate command allows you to generate default pipelines for languages Go, Java, or Node.

```sh
NAME:
   vela generate pipe - Generate a vela pipeline in a directory

USAGE:
   vela generate pipe [command options] [arguments...]

DESCRIPTION:
   Use this command to generate a pipeline
```

## Flags

```sh
OPTIONS:
   --type value, -t value  Type of generic pipeline to be generated. (go|node|java)
   --path value, -p value  Filename to use to create the secret or secrets
   --stages, -s            Define if the pipeline should be generated with stages
```

## Examples

```sh
EXAMPLES:
 1. Generate a vela pipeline in your current directory."
    $ vela generate pipe
 2. Generate a vela pipeline in a current directory."
    $ vela generate pipe -path /path/to/dir/
 3. Generate a node vela pipeline in current directory."
    $ vela generate pipe -type node
 4. Generate a java vela pipeline in current directory."
    $ vela generate pipe -type java
 5. Generate a go vela pipeline in a current directory."
    $ vela generate pipe -type go
 6. Generate a vela pipeline with stages in current directory."
    $ vela generate pipe -stages
```

## Sample

```
vela gen

".vela.yml" go pipeline generated.
```

```
vela gen -p ./test/ -t java

"./test/.vela.yml" java pipeline generated
```
