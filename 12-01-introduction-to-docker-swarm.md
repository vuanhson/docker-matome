# Introduction to docker swarm

In this lesson, we'll look at the highlights of Docker Swarm before we start working with it.

## Swarm 101
Swarm has two major components:
- An enterprise grade secure cluster:
  - Manage one or more Docker nodes as a cluster
  - Encrypted distributed cluster store
  - Encrypted networks
  - Secure join tokens
- An orchestration engine for creating mircoservices:
  - API for deploying and managing microservices
  - Declarative manifest files for defining apps
  - Provides availability to scale apps, and perform rolling updates and rollbacks

Swarm was initially a separate product layered on Docker, since Docker 1.12 it has become a part of the engine.

## The Cluster
- A swarm consists of one or more Docker nodes.
- Nodes are either a managers or a worker.
- Managers:
  - Manage the state of the cluster
  - Dispatch tasks to workers
- Workers:
  - Accepts and execute tasks
- State is held in etcd
- Swarm uses Transport Layer Security (TLS):
  - Encrypted communication
  - Authenticated nodes
  - Authorized roles
## Orchestration
- The atomic unit of scheduling is a swarm service.
- The service construct adds the following to a container:
  - scaling
  - rolling updates
  - rollback
  - updates
- A container wrapped in a service is a task or a replica.
