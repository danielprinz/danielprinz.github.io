---
title: What you need to know about Java and Docker
layout: post
categories: tools
---

## Why should I adapt Docker?
Docker is here since 2013 and it seems like everyone is using it. The benefit of having the same environment the local machine, on the staging environment and in production is huge!
The same java version is ensured, and by tagging the docker image it is versioned in a nice way.

That seems like a very big improvement, and it is. But there are also some pitfalls that I would like to mention. Especially for migrating older systems to docker.

## Update Java!
If possible, use Java 11. There the docker container support is enabled by default and the JVM will be aware of running inside a docker container.
The second best option is to run on the latest [Java 8 Update 191](https://www.oracle.com/technetwork/java/javase/8u191-relnotes-5032181.html) version. There the container support features have been backported and should behave the same.

If the application still runs on an older java version, at least [Java 8 Update 131](https://blogs.oracle.com/java-platform-group/java-se-support-for-docker-cpu-and-memory-limits) is required.  The two flags `-XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap` can be added on startup and the JVM will recognize the resource limits of the Container.

## What if I use an older Java version?
Older java versions are not aware of the docker container resource limits. This may not be a problem if it is ensured that the docker container has no resource limits, but in reality most of the time many containers are running on one machine. So this would lead to multiple containers competing for the same resources. Especially on load this will cause issues.