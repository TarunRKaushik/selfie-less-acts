# selfie-less-acts
A containerized web application build using flask and docker

The web app uses a microservice architecture along with an orchestrator to ensure robust and efficient functioning of the servers.

## Installation

Docker must be installed on the server-system before the application can be run on it.
https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce


Flask module along with flask_cors must be installed in the pythoon environment used.
```
pip install flask
pip install flask_cors
```


## Execution

Each of the containers can be placed in separate servers to maintain microservice architecture.
For fault tolerance and scalability, the acts server is maintained by running on multiple containers which are increased or decreased depending on the need for scaling up or down.
To maintain persistant data among all running containers, the data contained in each container, ```/static``` is stored in a docker volume

https://docs.docker.com/storage/volumes/


Build both the images by navigating to the folders 'actscontainer' and 'usercontainer' and running:
```
docker build .
```
After the image of the container is built, run the container using:
```
docker run <imageid> -p <req_port>:8000
```
The image_id is displayed at the end of the build process.
The req_port corresponds to the port number where the application needs to listen at.

Next the orchestrator needs to be run on the same server as the acts-container. By default, the orchestrator listens at port 80. This can be changed in the source code of orchestrator.py by changing the ```app.run()``` function's parameters.
Run the orchestrator using
```
python orchestrator.py
```

If the servers are cloud based, such as amazon ec2 instances, it would be ideal to use an aws load balancer to forward requests to the orchestrator on one instance and the acts container on the other one.
