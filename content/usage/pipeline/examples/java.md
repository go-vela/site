---
title: "Java"
toc: true
weight: 2
description: >
  Sample Java Pipeline
---

```yaml
version: "1"

steps:
  - name: install
    image: openjdk:8-alpine
    pull: true
    environment:
      GRADLE_USER_HOME: .gradle
      GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
    commands:
      - ./gradlew downloadDependencies

  - name: test
    image: openjdk:8-alpine
    pull: true
    environment:
      GRADLE_USER_HOME: .gradle
      GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
    commands:
      - ./gradlew test

  - name: build
    image: openjdk:8-alpine
    pull: true
    environment:
      GRADLE_USER_HOME: .gradle
      GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
    commands:
      - ./gradlew build
```
