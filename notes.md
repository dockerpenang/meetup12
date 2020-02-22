# Meetup#12

Github project - https://github.com/sujaypillai/hello.git

## Docker build problems
* Slower than local compilation
* Simplistic caching
* Requires root
* Secrets
* Dockerfile stopped evolving


## Buildkit
|Descripton                   | Link |
|---------------------------|-------------------------------------------|
|Proposal                   | https://github.com/moby/moby/issues/32925 |
|Development                | https://github.com/moby/buildkit          |

* Fundamental rewrite of backend
* Still the same client/server model
* Intermediate Representation
  * LLB
* Intermediate format for compiler [Dockerfile are really code]
* Similar idea to LLVM IR [JAVA - bytecode :: .NET - CIL
* Forms a graph [DAG - Directed Acyclic Graph]
* Frontends 
* Build parallelism, mount options, output formats, distributable workers, cross-compilation, rootless execution, bake
  
## Difference in normal build and using buildkit
> Normal docker build     `docker build -t sujaypillai/hello .`

> Using buildkit          `DOCKER_BUILDKIT=1 docker build -t sujaypillai/hello .`

Add the below line in  - `/etc/docker/daemon.json`
```
{ "features": { "buildkit": true } }
```

## Create a new builder
`docker buildx create -name meetupbuilder`

## Build multiplatform images
`docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t sujaypillai/hello --push .`

## Push local build caches to remote registry
`docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t sujaypillai/hello --push --cache-to=type=registry,ref=docker.io/sujaypillai/hello .`

## DockerTip - Check the platform support for any docker image
`docker container run mplatform/mquery sujaypillai/hello`


## buildctl [BuildKit ]
`brew install buildkit`
