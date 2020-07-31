# Managing swarm node

In this lesson, we learn how to manage the nodes in the swarm.

Docker node commands:
- `demote`: Demotes one or more nodes from manager in the swarm
- `inspect`: Displays detailed information on one or more nodes
- `ls`: Lists nodes in the swarm
- `promote`: Promotes one or more nodes to manager in the swarm
- `ps`: Lists tasks running on one or more nodes, defaults to current node
- `rm`: Removes one or more nodes from the swarm
- `update`: Updates a node

Docker swarm commands:

- `ca`: Displays and rotate the root CA
- `init`: Initializes a swarm
- `join`: Joins a swarm as a node and/or manager
- `join-token`: Manages join tokens
- `leave`: Leaves the swarm
- `unlock`: Unlocks swarm
- `unlock-key`: Manages the unlock key
- `update`: Updates the swarm

Managing swarm nodes:
Listing nodes:
```
docker node ls
```

Inspecting a node:
```
docker node inspect [NODE_NAME]
```

Promoting a worker to a manager:
```
docker node promote [NODE_NAME]
```

Demoting a manager to a worker:
```
docker node demote [NODE_NAME]
```

Removing a node form the swarm (node must be demoted first):
```
docker node rm -f [NODE_NAME]
```

After rm, the node still think it in a swarm, so we need make a node leave the swarm, execute from removed node:
```
docker swarm leave
```

Getting the join-token:
```
docker swarm join-token [worker|manager]
```

Make the node rejoin the swarm:
```
docker swarm join --token [TOKEN] \
<PRIVATE_IP>:2377
```

Usually promote other node to manager when take other manager maintenance