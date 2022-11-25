# Run SonarQube in a container on a ARM-based Mac

As of November 2022, the official Docker image for SonarQube does not support the AArch64 architecture (arm64) as used for instance on Apple MacBook with an M1 chip. 

This article illustrates a workaround for that limitation. 

Podman is used to start a virtual machine that can host your x86_64 or arm64 containers.

This guide has been tested on an Apple MacBook with an M1 chip but should work similarly well on more recent chips such as the M2

Introducing Podman

Podman is an alternative solution to the Docker engine that is becoming more and more popular in the containerization world. It is backed by Red Hat, which uses Podman it in Openshift, its Kubernetes distribution.

One of the advantages of Podman is that there is no more daemon. All containers are launched by runC without depending on a single process. Second, Podman was designed with to work hand in hand with Kubernetes. Podman can use the YAML manifests of Kubernetes. Both to launch Pods or generate manifests from an existing Pod. Podman is not capable of building container images. You will need other programs such as Buildah to create container images. This is an intentional choice by the Podman team, who did not design Podman as a monolithic application

Podman replaces the docker command line. The compatibility is such that you can create an alias so that you don’t have to change your habits or even your scripts.

Like Docker, Podman uses specific Linux kernel features to create containers and therefore necessitates a Linux VM on non-Linux machines: *podman machine*

* Podman machine consists of the following components: 

* QEMU plus HVF: Virtualization software

* Fedora CoreOS: The virtualized Linux distribution

* Ignition: Configuration management software for Fedora

* gvisor-tap-vsock: Arranges port mapping from VM to host machine
