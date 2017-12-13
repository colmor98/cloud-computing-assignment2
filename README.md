# cloud-computing-assignment2

C15502723
Colm O'Reilly

# Eternal IP
146.148.7.86 

# YouTube link
https://www.youtube.com/watch?v=0LfR5Pvob9k&feature=youtu.be&hd=1

# API
uses localhost:8080

# GET/ images
Returns a json array of all images.

Docker equivalent: docker images

Example call

curl -s -X GET -H 'Accept: application/json' http://localhost:8080/images | python -mjson.tool

# GET /containers?state=running
Returns a json array of all running containers on the vm.

Docker equivalent: docker ps

Example call

curl -s -X GET -H 'Accept: application/json' http://localhost:8080/containers?state=running | python -mjson.tool

# GET /containers/<id>
Returns a json object containing details about a container.

Docker equivalent: docker inspect <id>

Example call

curl -s -X GET -H 'Accept: application/json' http://localhost:8080/containers/b6cd8ea512c8  | python -mjson.tool

# GET /containers/<id>/logs
Returns a json object containing the logs of a container.

Docker equivalent: docker logs <id>

Example call
curl -s -X GET -H 'Accept: application/json' http://localhost:8080/containers/b6cd8ea512c8/logs  | python -mjson.tool

# GET /nodes
Returns a json array of all nodes in the swarm.

Docker equivalent: docker node ls

Example call

curl -s -X GET -H 'Accept: application/json' http://localhost:8080/nodes | python -mjson.tool

# GET /services
Returns a json array of all services running in the swarm.

Docker equivalent: docker service ls

Example call

curl -s -X GET -H 'Accept: application/json' http://localhost:8080/nodes | python -mjson.tool

# POST /images
Accepts an uploaded file, saves it as a Dockerfile and builds an image from it. Returns the id of the created image

Docker equivalent: docker build -t upload .

Example call

curl -H 'Accept: application/json' -F file=@Dockerfile http://localhost:8080/images

#POST /containers
Accepts json containing an image id. Runs a container with using that image id

Docker equivalent: docker run -d <imageid>

Example call

curl -X POST -H 'Content-Type: application/json' http://localhost:8080/containers -d '{"image": "b14752a6590e"}'

# PATCH /containers/<id>
Accepts json containing an a new state. Restarts or stops the docker container based on the state uploaded

Docker equivalents: docker stop, docker restart

Example call
curl -X PATCH -H 'Content-Type: application/json' http://localhost:8080/containers/b6cd8ea512c8 -d '{"state": "stopped"}'

# PATCH /images/<id>
Accepts json containing an a new tag. Tags the image with the new tag

Docker equivalent: docker tag <id>

Example call
curl -s -X PATCH -H 'Content-Type: application/json' http://localhost:5000/images/7f2619ed1768 -d '{"tag": "test:1.0"}'

# DELETE /images/<id>
Deletes the image specified

Docker equivalent: docker rmi <id>

Example call

 curl -s -X DELETE -H 'Accept: application/json' http://localhost:8080/images/7f2619ed1768
 
 # DELETE /container/<id>
Deletes the container specified

Docker equivalent: docker rm <id>

Example call

 curl -s -X DELETE -H 'Accept: application/json' http://localhost:8080/container/b6cd8ea512c8 
 
 # DELETE /container
Deletes all containers

Docker equivalent: docker rm $(docker ps -a -q)

Example call

 curl -s -X DELETE -H 'Accept: application/json' http://localhost:8080/container/
 
 # DELETE /images
Deletes all containers

Docker equivalent: docker rmi $(docker images -q)

Example call

 curl -s -X DELETE -H 'Accept: application/json' http://localhost:8080/container/
 
 
 # Running NGINX as service in Docker Swarm
 
 docker service create -d --replicas 3 -p 80:80 nginx
 
Creates a service running 3 replicas. Is detached from the terminal. Redirects traffic received on port 80 to port 80 in the service. Uses image nginx
