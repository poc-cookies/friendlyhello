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

List the machines and get their IP addresses:
	
	docker-machine ls

Run service / scale the app:
	
	docker stack deploy -c docker-compose.yml <service_name>
	docker stack deploy -c docker-compose.yml getstartedlab
	(no need to tear the stack down first or kill any containers)

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
