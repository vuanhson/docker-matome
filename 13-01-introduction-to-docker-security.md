# Introduction to docker security

We'll begin exploring ways to secure Docker by using security features native to both the operating system and Docker itself.

## Docker Security 101
Security is all about layers

Linux security:
- Namespaces
- Control Groups
- Mandatory Access Control (MAC)
- Seccomp

Docker security:
- Docker Swarm
- Docker Content Trust
- Docker Security Scanner
- Docker secrets

## Namespaces
Docker creates a set of namespaces and control groups for the container. Docker containers are an organized collections of namespaces.
- Namespaces provide isolation.
- Each container also gets its own network stack.

Docker on Linux namespaces:
- Process ID (pid)
- network (net)
- Filesystem/mount (mount)
- Inter-process Communication (ipc)
- User (user)
- UTS (uts)

## Control Groups
Control Groups are about setting limits for:
- CPU
- RAM
- Disk I/O
They help to mitigate denial-of-service attacks, and are important on multi-tenant platforms.

## Capabilities
Capabilities turn the binary “root/non-root” dichotomy into a fine-grained access control system. In most cases, containers do not need “real” root privileges at all. This means root within a container has much less privileges than the real root. It also means that even if an intruder manages to escalate to root within a container, it is much harder to do serious damage, or to escalate to the host.

## Mandatory Access Control systems
Two major MAC technologies are:
- SELinux
- AppArmor

## Seccomp
This limits the syscalls a container can make to the host's kernel. All new containers get a default seccomp configured

## Docker Swarm
Swarm Mode:
- Cryptographic node Ids
- Mutual authentication via TLS
- Secure join tokens
- CA configuration with automatic certificate rotation
- Encrypted cluster store
- Encrypted networks

```
docker swarm update --cert-expiry [INT]h
```

## Docker Secrets
These store sensitive data like:
- Passwords
- TLS Certificates
- API Keys

Secrets Workflow:
1. A secret is created and posted to the Swarm.
2. The secret is encrypted and stored.
3. A service is created and the secret is attached.
4. Secrets are stored in-flight.
5. The secret is mounted into the container of a service.
6. When the task is complete, the in-memory is torn down.
