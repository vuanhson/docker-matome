# Networking overview

In this lesson, we will go over the components and theory of how networking functions in Docker.

## Docker Networking 101
Docker Networking Component: 
- Open-source pluggable architecture
- Container Network Model (CNM) The CNM is a design specifications and it outlines the fundamental building blocks of a Docker network.
- `libnetwork` implements CNM: it is the real world implementation of the CNM and ultimately this is what Docker uses, and this is the implementation that docker uses for connecting containers. Libnetwork is also responsible for service discovery, ingress based container load balancing, and the network and management control plane functionality.
- Drivers extend the network topologies

Network Drivers:
- bridge (default)
- host
- overlay (distribute network among multiple docker host)
- macvlan (Assign mac to container, appearance of being a physical device on your network)
- none (disable networking, usually use in conjunction with custom network driver, cannot use with a swarm service)
- Network plugins

## Container Network Model
Defines three building blocks:
- Sandboxes: isolate network stack (interfaces, ports, routetable and DNS)
- Endpoints: Virtual network interface, connect sandbox to a network
- Networks: Software implementation of the 802.1 D bridge