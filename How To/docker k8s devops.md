Docker

Containers are just a process (or a group of processes) running in isolation, which is achieved with Linux namespaces and control groups. Linux namespaces and control groups are features that are built into the Linux kernel. Other than the Linux kernel itself, there is nothing special about containers.

What makes containers useful is the tooling that surrounds them. The labs in this course use Docker, which has been the understood standard tool for using containers to build applications. Docker provides developers and operators with a friendly interface to build, ship, and run containers on any environment.

top is a Linux utility that prints the processes on a system and orders them by resource consumption. Notice that there is only a single process in this output: it is the top process itself. You don't see other processes from the host in this list because of the PID namespace isolation.

Containers use Linux namespaces to provide isolation of system resources from other containers or the host. The PID namespace provides isolation for process IDs. If you run top while inside the container, you will notice that it shows the processes within the PID namespace of the container, which is much different than what you can see if you ran top on the host.

Even though we are using the Ubuntu image, it is important to note that the container does not have its own kernel. It uses the kernel of the host and the Ubuntu image is used only to provide the file system and tools available on an Ubuntu system.

PID is just one of the Linux namespaces that provides containers with isolation to system resources. Other Linux namespaces include:
MNT: Mount and unmount directories without affecting other namespaces.
NET: Containers have their own network stack.
IPC: Isolated interprocess communication mechanisms such as message queues.
User: Isolated view of users on the system.
UTC: Set hostname and domain name per container.


Namespaces are a feature of the Linux kernel. However, Docker allows you to run containers on Windows and Mac. The secret is that embedded in the Docker product is a Linux subsystem. Docker open-sourced this Linux subsystem to a new project: LinuxKit.



DOCKER FOR ME
Building Blocks:
Namespace:  Resource Allocation
cgroups:  Resource Limitation

Docker – Containerized application
Hosting:
Docker Cloud – Deployable environment for images with its reqd. runtime bins, libs, dependencies along with cloud infrastructure.
Docker Registry – A service responsible for hosting and distributing images.
Docker Hub – A repository for all images of cloud either public or private.
Workstation:
Docker machine –  It is actual service
To virtualize HOST OS.
Create a virtual environment for Docker installation with docker engine.
Ability to connect to that virtual environment.
Run docker commands.
Docker Engine – It is used for building Docker images and creating Docker containers.
-  Docker Daemon (Server) – It is used to communicate and fetch images from Docker Hub. (command dockerd)
-   REST API – which specifies interfaces that programs can use to talk to the daemon and instruct it what to do.
-    Docker Client – Interactive terminal for command I/O (command docker)
Docker Compose - This is used to define applications using multiple Docker containers.
Docker Swarm – Clustering service/API & orchestrating containers in Docker.
How does Docker work?
References: https://docs.docker.com/engine/docker-overview/
To generate this message, Docker took the following steps:                    	
1.	The Docker client contacted the Docker daemon.                            	
2.	The Docker daemon pulled the "hello-world" image from the Docker Hub. (amd64) (dockerd)
$ docker pull hello-world:latest
3.	The Docker daemon created a new container from that image which runs executable that produces output
you are currently reading.            	
$ docker run -t hello-world:latest
The Docker daemon streamed that output to the Docker client, which sent it to your terminal.

Docker Machine use:
 $ docker-machine ls   #show hypervisor in use
 $ docker-machine env default    # default hypervisor
 $ docker-machine active   # hypervisor active 
 $ docker version              # docker client display engine and client details.

Let's start our Nginx Docker container with this command:
$ docker run --name docker-nginx -p 8080:80 nginx
run is the command to create a new container
The --name flag is how we specify the name of the container (if left blank one is assigned for us, like nostalgic_hopper from Step 2)
-p specifies the port we are exposing in the format of -p local-machine-port:internal-container-port. In this case we are mapping Port 80 in the container to Port 80 on the server
nginx is the name of the image on dockerhub (we downloaded this before with the pull command, but Docker will do this automatically if the image is missing)

$ docker run -p 8888:8080 tomcat




 Somewhat tricky for Redis on docker on Windows

Ref: https://blogs.msdn.microsoft.com/uk_faculty_connection/2017/02/21/containers-redis-running-redis-on-windows-with-docker/

https://www.attunix.com/insights/redis-docker-windows/

Download redis for windows: 
In first terminal, run this command:
$ docker run -p 6379:6379 redis:latest
Keep that terminal open.
In second terminal, run this command from redis windows:
> redis-cli -h 192.168.99.100

How to run mongodb over Docker only

Server
$ docker run -ti --publish 27017:27017 --name mongo-server mongo:3.6





Client

docker run -it --rm mongo mongo --host 192.168.99.100 mongo-client





$ docker run -p 5001:5000 -d python-hello-world
0b2ba61df37fb4038d9ae5d145740c63c2c211ae2729fc27dc01b82b5aaafa26

The -p flag maps a port running inside the container to your host. In this case, you're mapping the Python app running on port 5000 inside the container to port 5001 on your host. 

$ docker container logs [container id] 
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
172.17.0.1 - - [28/Jun/2017 19:35:33] "GET / HTTP/1.1" 200 -

The Dockerfile is used to create reproducible builds for your application. A common workflow is to have your CI/CD automation run docker image build as part of its build process. After images are built, they will be sent to a central registry where they can be accessed by all environments (such as a test environment) that need to run instances of that application. In the next section, you will push your custom image to the public Docker registry, which is the Docker Hub, where it can be consumed by other developers and operators.

To store on Docker hub,

$ docker login
$ docker tag python-hello-world mayurp7/python-hello-world
$ docker push mayurp7/python-hello-world
Change in file and run again same commands. 

There is a caching mechanism in place for pushing layers too. Docker Hub already has all but one of the layers from an earlier push, so it only pushes the one layer that has changed.

When you change a layer, every layer built on top of that will have to be rebuilt. Each line in a Dockerfile builds a new layer that is built on the layer created from the lines before it. 

This is why the order of the lines in your Dockerfile is important. You optimized your Dockerfile so that the layer that is most likely to change (COPY app.py /app.py) is the last line of the Dockerfile. Generally for an application, your code changes at the most frequent rate. This optimization is particularly important for CI/CD processes where you want your automation to run as fast as possible.

Important topic:

Understand image layers
One of the important design properties of Docker is its use of the union file system.
Consider the Dockerfile that you created before:

FROM python:3.6.1-alpine                     # base layer
RUN pip install flask                              # At Build time of container
CMD ["python","app.py"]                       # At run time of container
COPY app.py /app.py

Each of these lines is a layer. Each layer contains only the delta, or changes from the layers before it. To put these layers together into a single running container, Docker uses the union file system to overlay layers transparently into a single view.
Each layer of the image is read-only except for the top layer, which is created for the container. The read/write container layer implements "copy-on-write," which means that files that are stored in lower image layers are pulled up to the read/write container layer only when edits are being made to those files. Those changes are then stored in the container layer.
The "copy-on-write" function is very fast and in almost all cases, does not have a noticeable effect on performance. You can inspect which files have been pulled up to the container level with the docker diff command. For more information, see the command-line reference on the docker diff command.


Because image layers are read-only, they can be shared by images and by running containers. For example, creating a new Python application with its own Dockerfile with similar base layers will share all the layers that it had in common with the first Python application.



You can also see the sharing of layers when you start multiple containers from the same image. Because the containers use the same read-only layers, you can imagine that starting containers is very fast and has a very low footprint on the host.

You might notice that there are duplicate lines in this Dockerfile and the Dockerfile that you created earlier in this lab. Although this is a trivial example, you can pull common lines of both Dockerfiles into a base Dockerfile, which you can then point to with each of your child Dockerfiles by using the FROM command.
Image layering enables the docker caching mechanism for builds and pushes. For example, the output for your last docker push shows that some of the layers of your image already exist on the Docker Hub.

      $ docker push mayurp7/python-hello-world

The push refers to a repository [docker.io/jzaccone/python-hello-world]
94525867566e: Pushed 
64d445ecbe93: Layer already exists 
18b27eac38a1: Layer already exists 
3f6f25cd8b1e: Layer already exists 
b7af9d602a0f: Layer already exists 
ed06208397d5: Layer already exists 
5accac14015f: Layer already exists 
latest: digest: sha256:91874e88c14f217b4cab1dd5510da307bf7d9364bd39860c9cc8688573ab1a3a size: 1786

To look more closely at layers, you can use the docker image history command of the Python image you created.

$ docker image history python-hello-world

Remove the stopped containers by running docker system prune:

 $ docker system prune
WARNING! This will remove:
        - all stopped containers
        - all volumes not used by at least one container
        - all networks not used by at least one container
        - all dangling images
Are you sure you want to continue? [y/N] y
Deleted Containers:
0b2ba61df37fb4038d9ae5d145740c63c2c211ae2729fc27dc01b82b5aaafa26

Total reclaimed space: 300.3kB

Summary:
Use the Dockerfile to create reproducible builds for your application and to integrate your application with Docker into the CI/CD pipeline.
Docker images can be made available to all of your environments through a central registry. The Docker Hub is one example of a registry, but you can deploy your own registry on servers you control.
A Docker image contains all the dependencies that it needs to run an application within the image. This is useful because you no longer need to deal with environment drift (version differences) when you rely on dependencies that are installed on every environment you deploy to.
Docker uses of the union file system and "copy-on-write" to reuse layers of images. This lowers the footprint of storing images and significantly increases the performance of starting containers.
Image layers are cached by the Docker build and push system. There's no need to rebuild or repush image layers that are already present on a system.
Each line in a Dockerfile creates a new layer, and because of the layer cache, the lines that change more frequently, for example, adding source code to an image, should be listed near the bottom of the file.
Swarm
To run containers on a Docker Swarm, you need to create a service. A service is an abstraction that represents multiple containers of the same image deployed across a distributed cluster.
Your node consists of one manager node and two workers nodes. Managers handle commands and manage the state of the swarm. Workers cannot handle commands and are simply used to run containers at scale. By default, managers are also used to run containers.
All docker service commands for the rest of this lab need to be executed on the manager node (Node1).
Note: Although you control the swarm directly from the node in which its running, you can control a Docker swarm remotely by connecting to the Docker Engine of the manager by using the remote API or by activating a remote host from your local Docker installation (using the $DOCKER_HOST and $DOCKER_CERT_PATH environment variables). This will become useful when you want to remotely control production applications, instead of using SSH to directly control production servers.

Scale your service
In production, you might need to handle large amounts of traffic to your application, so you'll learn how to scale.
Update your service with an updated number of replicas.

 Use the docker service command to update the NGINX service that you created previously to include 5 replicas. This is defining a new state for the service.

	 $ docker service update --replicas=5 --detach=true nginx1
nginx1

1. When this command is run, the following events occur:
The state of the service is updated to 5 replicas, which is stored in the swarm's internal storage.
Docker Swarm recognizes that the number of replicas that is scheduled now does not match the declared state of 5.
Docker Swarm schedules 4 more tasks (containers) in an attempt to meet the declared state for the service.
2. This swarm is actively checking to see if the desired state is equal to actual state and will attempt to reconcile if needed.


Check the running instances.

 After a few seconds, you should see that the swarm did its job and successfully started 4 more containers. Notice that the containers are scheduled across all three nodes of the cluster. The default placement strategy that is used to decide where new containers are to be run is the emptiest node, but that can be changed based on your needs.

 $ docker service ps nginx1


 


Send a lot of requests to http://localhost:80.

 The --publish 80:80 parameter is still in effect for this service; that was not changed when you ran the docker service update command. However, now when you send requests on port 80, the routing mesh has multiple containers in which to route requests to. The routing mesh acts as a load balancer for these containers, alternating where it routes requests to.

 Try it out by curling multiple times. Note that it doesn't matter which node you send the requests. There is no connection between the node that receives the request and the node that that request is routed to.

 $ curl localhost:80
node3
$ curl localhost:80
node3
$ curl localhost:80
node2
$ curl localhost:80
node1
$ curl localhost:80
node1


 You should see which node is serving each request because of the useful --mount command you used earlier.

 Limits of the routing mesh: The routing mesh can publish only one service on port 80. If you want multiple services exposed on port 80, you can use an external application load balancer outside of the swarm to accomplish this.


Check the aggregated logs for the service.

 Another easy way to see which nodes those requests were routed to is to check the aggregated logs. You can get aggregated logs for the service by using the command docker service logs [service name]. This aggregates the output from every running container, that is, the output from docker container logs [container name].

 $ docker service logs nginx1


 

 Based on these logs, you can see that each request was served by a different container.

 In addition to seeing whether the request was sent to node1, node2, or node3, you can also see which container on each node that it was sent to. For example, nginx1.5 means that request was sent to a container with that same name as indicated in the output of the command docker service ps nginx1.
5. Reconcile problems with containers
In the previous section, you updated the state of your service by using the command docker service update. You saw Docker Swarm in action as it recognized the mismatch between desired state and actual state, and attempted to solve the issue.
The inspect-and-then-adapt model of Docker Swarm enables it to perform reconciliation when something goes wrong. For example, when a node in the swarm goes down, it might take down running containers with it. The swarm will recognize this loss of containers and will attempt to reschedule containers on available nodes to achieve the desired state for that service.
You are going to remove a node and see tasks of your nginx1 service be rescheduled on other nodes automatically.
To get a clean output, create a new service by copying the following line. Change the name and the publish port to avoid conflicts with your existing service. Also, add the --replicas option to scale the service with five instances:
 $ docker service create --detach=true --name nginx2 --replicas=5 --publish 81:80  --mount source=/etc/hostname,target=/usr/share/nginx/html/index.html,type=bind,ro nginx:1.12
aiqdh5n9fyacgvb2g82s412js



On node1, use the watch utility to watch the update from the output of the docker service ps command.

 Tip: watch is a Linux utility and might not be available on other operating systems.

 $ watch -n 1 docker service ps nginx2


 This command should create output like this:

 


Click node3 and enter the command to leave the swarm cluster:
 $ docker swarm leave


 Tip: This is the typical way to leave the swarm, but you can also kill the node and the behavior will be the same.


Click node1 to watch the reconciliation in action. You should see that the swarm attempts to get back to the declared state by rescheduling the containers that were running on node3 to node1 and node2 automatically.

 





















Kubernetes
Steps to run on Windows




Devops
DevOps is a set of software development practices that combines software development (Dev) and information technology operations (Ops) to shorten the systems development life cycle while delivering features, fixes, and updates frequently in close alignment with business objectives

From an academic perspective, Len Bass, Ingo Weber, and Liming Zhu—three computer science researchers from the CSIRO and the Software Engineering Institute—suggested defining DevOps as "a set of practices intended to reduce the time between committing a change to a system and the change being placed into normal production, while ensuring high quality"

Phases:

Coding – code development and review, source code management tools, code merging - GitHub
Building – continuous integration tools, build status  - Jenkins
Testing – continuous testing tools that provide quick and timely feedback on business risks - Selenium/Pytest
Packaging – artifact repository, application pre-deployment staging  - 
Releasing – change management, release approvals, release automation  - Jenkins 
Configuring – infrastructure configuration and management, infrastructure as code tools - Ansible
Monitoring – applications performance monitoring, end-user experience - Nagios

Infra Automation Tools”

Infrastructure as code — Ansible, Terraform, Puppet, Chef
CI/CD — Jenkins, TeamCity, Shippable, Bamboo, Azure DevOps
Test automation — Selenium, Cucumber, Apache JMeter
Containerization — Docker, Rocket, Unik
Orchestration — Kubernetes, Swarm, Mesos
Software deployment — Elastic Beanstalk, Octopus, Vamp
Measurement — NewRelic, Kibana, Datadog, DynaTrace
ChatOps — Hubot, Lita, Cog
