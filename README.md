# Getting Fun with Docker

## Terminology

`image`

	Executable package that includes everything needed to run an application (the code, a runtime, libraries, environment variables, and configuration files)
	
`container`

	Runtime instance of an image (what the image becomes in memory when executed)
	
`service`

	Container in production. A service only runs one image, but it codifies the way that image runs (what ports, replicas of the container, and so on)

`task`
	
	Single container running in a service

`swarm`

	Group of machines that are running Docker and joined into a cluster

`node`
	
	Physical or virtual machine joined to a swarm

`swarm manager`
	
	The only machine in a swarm that can execute your commands, or authorize other machines to join the swarm as workers

`worker`
	
	Machine that provides capacity and do not have the authority to tell any other machine what it can and cannot do

`stack`

    Group of interrelated services that share dependencies, and can be orchestrated and scaled together

## Commands

Docker version:

    docker --version

View Docker installation details:

    docker info

Create image using this directory's Dockerfile:

    docker build --tag=<tag_name> .

List all images:

	docker image ls

Execute image:
	
	docker run <image_name>
	docker run -d -p 4000:80 friendlyhello

Publish the image:
	
	docker push username/repository:tag

Stop container:
	
	docker container stop <container_id>

List all containers that are running:
	
	docker container ls

Enable swarm mode:
	
	docker swarm init

Run service / scale the app:
	
	docker stack deploy -c docker-compose.yml <service_name>
	docker stack deploy -c docker-compose.yml getstartedlab
	(no need to tear the stack down first or kill any containers)

List services:

    docker service ls

View tasks for a service:

    docker service ps <service>

View services associated with a stack:
	
	docker stack services <stack_name>
	docker stack services getstartedlab

View all tasks of a stack:
	
	docker stack ps <stack_name>
	docker stack ps getstartedlab

Take the app down:
	
	docker stack rm <stack_name>
	docker stack rm getstartedlab

Take down the swarm:
	
	docker swarm leave --force

List the machines and get their IP addresses:
	
	docker-machine ls

Send commands to your VMs:

    docker-machine ssh <machine_name> <command>

Instruct `myvm1` machine to become a swarm manager:

    docker-machine ssh myvm1 "docker swarm init --advertise-addr <myvm1 ip>"
    docker-machine ssh myvm1 "docker swarm init --advertise-addr 192.168.99.100"

Add `myvm2` machine as a worker to the swarm:

    docker-machine ssh myvm2 "docker swarm join --token <token> <ip>"

List nodes in the swarm:

    docker-machine ssh myvm1 "docker node ls"

Get the command to configure your shell to talk to `myvm1`:

    docker-machine env myvm1

Configure your shell to talk to `myvm1`:

    eval $(docker-machine env myvm1)

Unset the `docker-machine` environment variables in your current shell:

    eval $(docker-machine env -u)

Restart a machine that’s stopped:

    docker-machine start <machine-name>

## Docker Get Started Guide

[Get Started Guide](https://docs.docker.com/get-started/)
