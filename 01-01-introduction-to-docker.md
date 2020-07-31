# Introduction to docker

## Docker:
- The company Docker
- The container runtime and orchestration Engine (Most of the time)
- The opensource project Moby

### Docker, Inc.:

- Based in San Francisco
- Founded by Solomon Hykes
- Start as a PaaS provider called dotCloud
- dotCloud leveraged Linux containers
- Their internal tool used to manage containers was nick-named Docker
- In 2013 dotCloud was rebranded as Docker

### The Docker runtime and orchestration engine:

- Most people are referring to the Docker Engine
- Two main editions:
  - Enterprise Edition (EE): Allow access to certified docker image and plugin, same day support, vunerability skating... 
  - Community Edition (CE)
- Both are released quarterly:
  - CE is supported for 4 months
  - EE is supported for 12 months

### The Open-Source Project(Moby)

- The upstream project of Docker
- Breaks Docker down into more modular components
- Code is available on GitHub: https://github.com/moby/moby

## Why Use Docker?
Docker Use Cases:

- Dev/Prod parity:
  - Dev and Production environment are the same
  - Bugs in Production can be replicated in Development
- Simplifying Configuration:
  - Lets you put your environment and configuration into code and deploy it
  - Allows the same Docker configuration to be used in a variety of environments
  - Decouples infrastructure requirements from the application environment
- Code Pipeline Management: 
  - Build standards and repeatable processes (code - image - dev - stg - prod etc...)
- Developer Productivity (Easy when setting up local development environment)
- App Isolation (Security)
- Server Consolidation (Efficently use server resources)
- Debugging Capabilities (not fighting with difference between dev/prod)
- Multi-tenancy (Run multiple client same docker server without the fear of compromising their information)
