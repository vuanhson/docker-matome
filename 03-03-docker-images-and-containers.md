# Docker images and containers

## What are Docker images?

Docker Images:
- Files comprised of multiple layers
- Execute code in a Docker container
- Built from the instructions
- Use images to create an instance of a container

## Docker images and layers
- Image are made of multiple layers.
- Each layer represents an instruction in the image’s Dockerfile.
- Each layer except, the very last one, is read-only.
- Each layer is only a set of differences from the layer before it.
- Layers are stacked on top of each other.
- Containers add new writable layers on top of the underlying layers
- All changes made to a running container is made to the Container layer

## What are containers?
A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.

## Container and layers
- Top writable layer (this is main difference between container and image)
- All changes are stored in the writable layer
- The writable layer is deleted when the container is deleted
- The image remains unchanged
