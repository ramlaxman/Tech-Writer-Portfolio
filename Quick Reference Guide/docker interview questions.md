

Virtual Machines Vs Docker Containers
Virtual Machines
Docker Containers
Need more resources
Less resources are used
Process isolation is done at hardware level
Process Isolation is done at Operating System level
Separate Operating System for each VM
Operating System resources can be shared within Docker
VMs can be customized.
Custom container setup is easy
Takes time to create a Virtual Machine.
Creation of docker is very quick
Booting takes minutes
Booting is done within seconds


Q1) What is Docker?
Docker can be defined as Containerization platform that packs all your applications, all the necessary dependencies combined to form containers. This will not only ensure the applications work seamlessly given any environment but also provides better efficiency to your Production ready applications. Docker wraps up bits and pieces of software with all the needed filesystems containing everything that needs to run the code, provide the runtime, system tools / libraries. This will ensure that the software is always run and executed the same, regardless of the environment.
Docker is also a namespacing tool allow better control over processes’ use of system resources, making such tools extremely popular for use by PaaS providers
Containers run on the same machine sharing the same Operating system Kernel, this makes it faster – as starting the applications is the only time that is required to start your Docker container (remember that the OS Kernel is already UP and running and uses the least of the RAM possible).
Q2) What is the advantage of Docker over hypervisors?
Docker is light weight and more efficient in terms of resource uses because it uses the host underlying kernel rather than creating its own hypervisor.
Q3) How is Docker different from other container technologies?
To start with, Docker is one of the upcoming and is a fresh project. Since its inception has been done in the Cloud era, it is way better many of the other competing Container technologies which have ruled their way until Docker came into existence. There is an active community that is running towards the better upbringing of Docker and it has also started extending its support to Windows and Mac OSX environments in the recent days. Other than these, below are the best possible reasons to highlight Docker as one of the better options to choose from than the existing Container technologies.
• There is no limitation on running Docker as the underlying infrastructure can be your laptop or else your Organization’s Public / Private cloud space
• Docker with its Container HUB forms the repository of all the containers that you are ever going to work, use and download. Sharing of applications is as well possible with the Containers that you create.
• Docker is one of the best documented technologies available in the Containerization space.


Q4) What is Docker image?
Docker image can be understood as a template from which Docker containers can be created as many as we want out of that single Docker image. Having said that, to put it in layman terms, Docker containers are created out of Docker images. Docker images are created with the build command, and this produces a container that starts when it is run. Docker images are stored in the Docker registry such as the public Docker registry (registry.hub.docker.com) as these are designed to be constituted with layers of other images, enabling just the minimal amount of data over the network.
Q5) What is Docker container?
This is a very important question so just make sure you don’t deviate from the topic and I will advise you to follow the below mentioned format:
1. Docker containers include the application and all of its dependencies, but share the kernel with other containers, running as isolated processes in user space on the host operating system. Docker containers are not tied to any specific infrastructure: they run on any computer, on any infrastructure, and in any cloud.
2. Now explain how to create a Docker container, Docker containers can be created by either creating a Docker image and then running it or you can use Docker images that are present on the Dockerhub.
3. Docker containers are basically runtime instances of Docker images.
Q6) What is Docker hub?
Docker hub is a cloud-based registry service which allows you to link to code repositories, build your images and test them, stores manually pushed images, and links to Docker cloud so you can deploy images to your hosts. It provides a centralized resource for container image discovery, distribution and change management, user and team collaboration, and workflow automation throughout the development pipeline.
Q7) What is Docker Swarm?
Docker Swarm can be best understood as the native way of Clustering implementation for Docker itself. Docker Swarm turns a pool of Docker hosts into a single and virtual Docker host. It serves the standard Docker API or any other tool that can already communicate with a Docker daemon can make use of Docker Swarm to scale in a transparent way to multiple hosts. Following are the list of some of the supported tools that will be helpful in achieving what we have discussed just now.
• Dokku
• Docker Compose
• Docker Machine
• Jenkins
Q8) What is Dockerfile used for?
Dockerfile is nothing but a set of instructions that have to be passed on to Docker itself, so that it can build images automatically reading these instructions from that specified Dockerfile. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using docker build users can create an automated build that executes several command-line instructions in succession.


Q9) Can I use JSON instead of YAML/YML for my compose file in Docker?
YES, you can very comfortably use JSON instead of the default YAML for your Docker compose file. In order to use JSON file with compose, you need to specify the filename to use as the following:
docker-compose -f docker-compose.json up
Q10) Tell us how you have used Docker in your past position?
This is a question that you could bring upon your whole experience with Docker and if you have used any other Container technologies before Docker. You could also explain the ease that this technology has brought in the automation of the development to production lifecycle management. You can also discuss about any other integrations that you might have worked along with Docker such as Puppet, Chef or even the most popular of all technologies – Jenkins. If you do not have any experience with Docker itself but similar tools from this space, you could convey the same and also show in your interest towards learning this leading containerization technology.
Q11) How to create Docker container?
You can create a Docker container out of any specific Docker image of your choice and the same can be achieved using the command given below:

$ docker run -t -i command name

The command above will create the container and also starts it for you. In order to check whether the Docker container is created and whether it is running or not, you could make use of the following command. This command will list out all the Docker containers along with its statuses on the host that the Docker container runs.
$ docker ps -a
Q12) How to stop and restart the Docker container?
The following command can be used to stop a certain Docker container with the container id as
CONTAINER_ID:
docker container stop CONTAINER_ID
The following command can be used to restart a certain Docker container with the container id as
CONTAINER_ID:
docker container restart CONTAINER_ID
Q13) How far do Docker containers scale?
Best examples in the Web deployments like Google, Twitter and best examples in the Platform Providers like Heroku, dotCloud run on Docker which can scale from the ranges of hundreds of thousands to millions of containers running in parallel, given the condition that the OS and the memory doesn’t run out from the hosts which runs all these innumerable containers hosting your applications.
Q14) What platforms does Docker run on?
Docker is currently available on the following platforms and also on the following Vendors or Linux:
• Ubuntu 12.04, 13.04
• Fedora 19/20+
• RHEL 6.5+
• CentOS 6+
• Gentoo
• ArchLinux
• openSUSE 12.3+
• CRUX 3.0+
Docker is currently available and also is able to run on the following Cloud environment setups given as below:
• Amazon EC2
• Google Compute Engine
• Microsoft Azure
• Rackspace
Docker is extending its support to Windows and Mac OSX environments and support on Windows has been on the growth in a very drastic manner.
Q15) Do I lose my data when the Docker container exits?
There is no loss of data when any of your Docker containers exits as any of the data that your application writes to the disk in order to preserve it. This will be done until the container is explicitly deleted. The file system for the Docker container persists even after the Docker container is halted.
Q16) What, in your opinion, is the most exciting potential use for Docker?
The most exciting potential use of Docker that I can think of is its build pipeline. Most of the Docker professionals are seen using hyper-scaling with containers, and indeed get a lot of containers on the host that it actually runs on. These are also known to be blatantly fast. Most of the development – test build pipeline is completely automated using the Docker framework.
Q17) Why is Docker the new craze in virtualization and cloud computing?
Docker is the newest and the latest craze in the world of Virtualization and also Cloud computing because it is an ultra-lightweight containerization app that is brimming with potential to prove its mettle.
Q18) Why do my services take 10 seconds to recreate or stop?
Docker compose stop will attempt to stop a specific Docker container by sending a SIGTERM message. Once this message is delivered, it waits for the default timeout period of 10 seconds and once the timeout period is crossed, it then sends out a SIGKILL message to the container – in order to kill it forcefully. If you are actually waiting for the timeout period, then it means that the containers are not shutting down on receiving SIGTERM signals / messages.
In an attempt to solve this issue, the following is what you can do:
• You can ensure that you are using the JSON form of the CMD and also the ENTRYPOINT in your dockerfile.
• Use [“program”, “argument1”, “argument2”] instead of sending it as a plain string as like this – “program argument1 argument2”.
• Using the string form, makes Docker run the process using bash that can’t handle signals properly. Compose always uses the JSON form.
• If it is possible then modify the application which you intend to run by adding an explicit signal handler for the SIGTERM signal
• Also set the stop_signal to a proper signal that the application can understand and also know how to handle it.
http://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/
Use RUN instructions to build your image by adding layers on top of initial image.
Prefer ENTRYPOINT to CMD when building executable Docker image and you need a command always to be executed. 
Additionally use CMDif you need to provide extra default arguments that could be overwritten from command line when docker container runs.Choose CMD if you need to provide a default command and/or arguments that can be overwritten from command line when docker container runs.

Q19) How do I run multiple copies of a Compose file on the same host?
Docker’s compose makes use of the Project name to create unique identifiers for all of the project’s containers and resources. In order to run multiple copies of the same project, you will need to set a custom project name using the –p command line option or you could use the COMPOSE_PROJECT_NAME environment variable for this purpose.
Q20) What’s the difference between up, run, and start?
On any given scenario, you would always want your docker-compose up. Using the command UP, you can start or restart all the services that are defined in a docker-compose.yml file. In the “attached” mode, which is also the default mode – we will be able to see all the log files from all the containers. In the “detached” mode, it exits after starting all the containers, which continue to run in the background showing nothing over in the foreground.
Using docker-compose run command, we will be able to run the one-off or the ad-hoc tasks that are required to be run as per the Business needs and requirements. This requires the service name to be provided which you would want to run and based on that, it will only start those containers for the services that the running service depends on. Using the run command, you can run your tests or perform any of the administrative tasks as like removing / adding data to the data volume container. It is also very similar to the docker run –ti command, which opens up an interactive terminal to the containers an exit status that matches with the exit status of the process in the container.
Using the docker-compose start command, you can only restart the containers that were previously created and were stopped. This command never creates any new Docker containers on its own.

Q21) What’s the benefit of “Dockerizing?”
Dockerizing enterprise environments helps teams to leverage over the Docker containers to form a service platform as like a CaaS (Container as a Service). It gives teams that necessary agility, portability and also lets them control staying within their own network / environment.
Most of the developers opt to use Docker and Docker alone because of the flexibility and also the ability that it provides to quickly build and ship applications to the rest of the world. Docker containers are portable and these can run on any environment without making any additional changes when the application developers have to move between Developer, Staging and Production environments. This whole process is seamlessly implemented without the need of performing any recoding activities for any of the environments. These not only helps reduce the time between these lifecycle states, but also ensures that the whole process is performed with utmost efficiency. There is every possibility for the Developers to debug any certain issue, fix it and also update the application with it and propagate this fix to the higher environments with utmost ease.
The operations teams can handle the security of the environments while also allowing the developers build and ship the applications in an independent manner. The CaaS platform that is provided by Docker framework can deploy on-premise and is also loaded with full of enterprise level security features such as role-based access control, integration with LDAP or any Active Directory, image signing and etc. Operations teams have heavily rely on the scalability provided by Docker and can also leverage over the Dockerized applications across any environments.
Docker containers are so portable that it allows teams to migrate workloads that run on an Amazon’s AWS environment to Microsoft Azure without even having to change its code and also with no downtime at all. Docker allows teams to migrate these workloads from their cloud environments to their physical datacenters and vice versa. This also enables the Organizations to focus on the infrastructure from the gained advantages both monetarily and also the self-reliability over Docker. The lightweight nature of Docker containers compared to traditional tools like virtualization, combined with the ability for Docker containers to run within VMs, allowing teams to optimize their infrastructure by 20X, and save money in the process.
Q22) How many containers can run per host?
Depending on the environment where Docker is going to host the containers, there can be as many containers as the environment supports. The application size, available resources (like CPU, memory) will decide on the number of containers that can run on an environment. Though containers create newer CPU on their own but they can definitely provide efficient ways of utilizing the resources. The containers themselves are super lightweight and only last as long as the process they are running.
Q23) Is there a possibility to include specific code with COPY/ADD or a volume?
This can be easily achieved by adding either the COPY or the ADD directives in your dockerfile. This will count to be useful if you want to move your code along with any of your Docker images, example, sending your code an environment up the ladder – Development environment to the Staging environment or from the Staging environment to the Production environment. 
Having said that, you might come across situations where you’ll need to use both the approaches. You can have the image include the code using a COPY, and use a volume in your Compose file to include the code from the host during development. The volume overrides the directory contents of the image.
Q24) Will cloud automation overtake containerization any sooner?
Docker containers are gaining the popularity each passing day and definitely will be a quintessential part of any professional Continuous Integration / Continuous Development pipelines. Having said that there is equal responsibility on all the key stakeholders at each Organization to take up the challenge of weighing the risks and gains on adopting technologies that are budding up on a daily basis. In my humble opinion, Docker will be extremely effective in Organizations that appreciate the consequences of Containerization.
Q25) Is there a way to identify the status of a Docker container?
We can identify the status of a Docker container by running the command ‘docker ps –a’, which will in turn list down all the available docker containers with its corresponding statuses on the host. From there we can easily identify the container of interest to check its status correspondingly.
Q26) What are the differences between the ‘docker run’ and the ‘docker create’?
The most important difference that can be noted is that, by using the ‘docker create’ command we can create a Docker container in the Stopped state. We can also provide it with an ID that can be stored for later usages as well.
This can be achieved by using the command ‘docker run’ with the option –cidfileFILE_NAME as like this:
‘docker run –cidfileFILE_NAME’
Q27) What are the various states that a Docker container can be in at any given point in time?
There are four states that a Docker container can be in, at any given point in time. Those states are as given as follows:
• Running
• Paused
• Restarting
• Exited
Q28) Can you remove a paused container from Docker?
To answer this question blatantly, No, it is not possible to remove a container from Docker that is just paused. It is a must that a container should be in the stopped state, before it can be removed from the Docker container.
Q29) Is there a possibility that a container can restart all by itself in Docker?
To answer this question blatantly, No, it is not possible. The default –restart flag is set to never restart on its own. If you want to tweak this, then you may give it a try.
Q30) What is the preferred way of removing containers - ‘docker rm -f’ or ‘docker stop’ then followed by a ‘docker rm’?
The best and the preferred way of removing containers from Docker is to use the ‘docker stop’, as it will allow sending a SIG_HUP signal to its recipients giving them the time that is required to perform all the finalization and cleanup tasks. Once this activity is completed, we can then comfortably remove the container using the ‘docker rm’ command from Docker and thereby updating the docker registry as well.
Q31) Difference between Docker Image and container?
Docker container is the runtime instance of docker image.
Docker Image doesnot have a state and its state never changes as it is just set of files whereas docker container has its execution state.
Is Container technology new?
No, it is not. Different variations of containers technology were out there in *NIX world for a long time.Examples are:-Solaris container (aka Solaris Zones)-FreeBSD Jails-AIX Workload Partitions (aka WPARs)-Linux OpenVZ
What are the networks that are available by default?
Bridge
It is the default network all containers connect to if you don’t specify the network yourself
None
connects to a container-specific network stack that lacks a network interface
Host
connects to the host’s network stack – there will be no isolation between the host machine and the container, as far as network is concerned


What is the use case for Docker?
Well, I think, docker is extremely useful in development environments. Especially for testing purposes. You can deploy and re-deploy apps in a blink of an eye.
Also, I believe there are use cases where you can use Docker in production. Imagine you have some Node.js application providing some services on the web. Do you need to run full OS for this?
Eventually, if docker is good or not should be decided on an application basis. For some apps, it can be sufficient, for others not.
How exactly are containers (Docker in our case) different from hypervisor virtualization (vSphere)? What are the benefits?
To run an application in a virtualized environment (e.g., vSphere), we first need to create a VM, install an OS inside and only then deploy the application. To run the same application in docker, all you need is to deploy that application in Docker. There is no need for additional OS layer. You just deploy the application with its dependent libraries, docker engine (kernel, etc.) provides the rest.This table from a Docker official website shows it in a quite clear way.

Another benefit of Docker, from my perspective, is speed of deployment. Let’s imagine a scenario:
ACME inc. needs to virtualize application GOOD APP for testing purposes.
Conditions are:
Application should run in an isolated environment.
Application should be available to be redeployed at any moment in a very fast manner.
Solution 1.
In vSphere world what we would usually do, is:
Deploy OS in a VM running on vSphere.
Deploy an application inside OS.
Create a template.
Redeploy the template in case of need. Time of redeployment around 5-10 minutes.
Sounds great! Having app up and running in an hour and then being able to redeploy it in 5 minutes.

Solution 2.
Deploy Docker.
Deploy the app GOODAPP in container.
Redeploy the container with an app when needed.
Benefits: No need of deploying full OS for each instance of the application. Deploying a container takes seconds.

How did you become involved with the Docker project?
I came across Docker not long after Solomon open sourced it. I knew a bit about LXC and containers (a past life includes working on Solaris Zones and LPAR on IBM hardware too), and so I decided to try it out. I was blown away by how easy it was to use. My prior interactions with containers had left me with the feeling they were complex creatures that needed a lot of tuning and nurturing. Docker just worked out of the box. Once I saw that and then saw the CI/CD-centric workflow that Docker was building on top I was sold.
Docker is the new craze in virtualization and cloud computing. Why are people so excited about it?
Available for all platforms now
Easy to use due to great examples in Docker Docs
People used github can get used to with Docker on faster pace
Blazing speed for testing and implementation
Easy to deploy on private to hybrid clouds like AWS, openstack.
I think it’s the lightweight nature of Docker combined with the workflow. It’s fast, easy to use and a developer-centric DevOps-ish tool. Its mission is basically: make it easy to package and ship code. Developers want tools that abstract away a lot of the details of that process. They just want to see their code working. That leads to all sorts of conflicts with Sys Admins when code is shipped around and turns out not to work somewhere other than the developer’s environment. Docker turns to work around that by making your code as portable as possible and making that portability user-friendly and simple.
Do you think open source development has heavily influenced cloud technology development?
I think open source software is closely tied to cloud computing. Both in terms of the software running in the cloud and the development models that have enabled the cloud. Open source software is cheap, it’s usually low friction both from an efficiency and a licensing perspective.
How do you think Docker will change virtualization and cloud environments? Do you think cloud technology has a set trajectory, or is there still room for significant change?
I think there are a lot of workloads that Docker is ideal for, as I mentioned earlier both in the hyper-scale world of many containers and in the dev-test-build use case. I fully expect a lot of companies and vendors to embrace Docker as an alternative form of virtualization on both bare metal and in the cloud.
As for cloud technology’s trajectory. I think we’ve seen a significant change in the last couple of years. I think they’ll be a bunch more before we’re done. The question of OpenStack and whether it will succeed as an IAAS alternative or DIY cloud solution. I think we’ve only touched on the potential for PAAS and there’s a lot of room for growth and development in that space. It’ll also be interesting to see how the capabilities of PAAS products develop and whether they grow to embrace or connect with consumer cloud-based products.



Can you give us a quick rundown of what we should expect from your Docker presentation at OSCON this year?
It’s very much a crash course introduction to Docker. It’s aimed at Developers and SysAdmins who want to get started with Docker in a very hands on way. We’ll teach the basics of how to use Docker and how to integrate it into your daily workflow.
Your bio says “for a real job” you’re the VP of Services for Docker. Do you consider your other open source work a hobby?
That’s mostly a joke related to my partner. Like a lot of geeks, I’m often on my computer, tapping away at a problem or writing something. My partner jokes that I have two jobs: my “real” job and my open source job. Thankfully over the last few years, at places like Puppet Labs and Docker, I’ve been able to combine my passion with my paycheck.
Why is Docker the new craze in virtualization and cloud computing?
It’s OSCON time again, and this year the tech sector is abuzz with talk of cloud infrastructure. One of the more interesting startups is Docker, an ultra-lightweight containerization app that’s brimming with potential
I caught up with the VP of Services for Docker, James Turnbull, who’ll be running a Docker crash course at the con. Besides finding out what Docker is anyway, we discussed the cloud, open source contributing and getting a real job.
Why do my services take 10 seconds to recreate or stop?
Compose stop attempts to stop a container by sending a SIGTERM. It then waits for a default timeout of 10 seconds. After the timeout, a SIGKILL is sent to the container to kill it forcefully. If you are waiting for this timeout, it means that your containers aren’t shutting down when they receive the SIGTERM signal.
There has already been a lot written about this problem of processes handling signals in containers.
To fix this issue, try the following:
Make sure you’re using the JSON form of CMD and ENTRYPOINT in your Dockerfile.
For example use ["program", "arg1", "arg2"]not"program arg1 arg2". Using the string form causes Docker to run your process using bash which doesn’t handle signals properly. Compose always uses the JSON form, so don’t worry if you override the command or entrypoint in your Compose file.
-If you are able, modify the application that you’re running to add an explicit signal handler for SIGTERM.
-Set the stop_signal to a signal which the application knows how to handle:
-web: build: . stop_signal: SIGINT
-If you can’t modify the application, wrap the application in a lightweight init system (like s6) or a signal proxy (like dumb-init or tini). Either of these wrappers take care of handling SIGTERM properly.



How do I run multiple copies of a Compose file on the same host?
Compose uses the project name to create unique identifiers for all of a project’s containers and other resources. To run multiple copies of a project, set a custom project name using the -p command line option or theCOMPOSE_PROJECT_NAME environment variable.
Docker Container Interview Questions
What is the base image required to build a Docker container?
The base image depends on the tool or script. You can pursue available images by searching Docker Hub for the domain (e.g., “biology”, “science”) and read the documentation for specific images.
Most frequently used CyVerse base images:
ubuntu:12.04
ubuntu:14.04
Can I use json instead of yaml for my Compose file?
Yes. Yaml is a superset of json so any JSON file should be valid Yaml. To use a JSON file with Compose, specify the filename to use, for example:
docker-compose -f docker-compose.json up 
Should I include my code with COPY/ADD or a volume?
You can add your code to the image using COPY or ADD directive in a Dockerfile. This is useful if you need to relocate your code along with the Docker image, for example when you’re sending the code to another environment (production, CI, etc).
You should use a volume if you want to make changes to your code and see them reflected immediately, for example when you’re developing code and your server supports hot code reloading or live-reload.
There may be cases where you’ll want to use both. You can have the image include the code using a COPY, and use a volume in your Compose file to include the code from the host during development. The volume overrides the directory contents of the image.
Where can I find example compose files?
There are many examples of Compose files on github.
Compose documentation
Installing Compose
Get started with Django
Get started with Rails
Get started with WordPress
Command line reference
Compose file reference
Are you operationally prepared to manage multiple languages/libraries/repositories?
Last year, we encountered an organization that developed a modular application while allowing developers to “use what they want” to build individual components. It was a nice concept but a total organizational nightmare — chasing the ideal of modular design without considering the impact of this complexity on their operations.
The organization was then interested in Docker to help facilitate deployments, but we strongly recommended that this organization not use Docker before addressing the root issues. Making it easier to deploy these disparate applications wouldn’t be an antidote to the difficulties of maintaining several different development stacks for long-term maintenance of these apps.
Do you already have a logging, monitoring, or mature deployment solution?
Chances are that your application already has a framework for shipping logs and backing up data to the right places at the right times. To implement Docker, you not only need to replicate the logging behavior you expect in your virtual machine environment, but you also need to prepare your compliance or governance team for these changes. New tools are entering the Docker space all the time, but many do not match the stability and maturity of existing solutions. Partial updates, rollbacks, and other common deployment tasks may need to be re-engineered to accommodate a containerized deployment.
If it’s not broken, don’t fix it. If you’ve already invested the engineering time required to build a continuous integration/continuous delivery (CI/CD) pipeline, containerizing legacy apps may not be worth the time investment.
Will cloud automation overtake containerization?
At AWS Re:Invent last month, Amazon chief technology officer Werner Vogels spent a significant portion of his keynote on AWS Lambda, an automation tool that deploys infrastructure based on your code. While Vogels did mention AWS’ container service, his focus on Lambda implies that he believes dealing with zero infrastructure is preferable to configuring and deploying containers for most developers.
Containers are rapidly gaining popularity in the enterprise, and are sure to be an essential part of many professional CI/CD pipelines. But as technology experts and CTOs, it is our responsibility to challenge new methodologies and services and properly weigh the risks of early adoption. I believe Docker can be extremely effective for organizations that understand the consequences of containerization — but only if you ask the right questions.
You say that Ansible can take up to 20x longer to provision, but why?
Docker uses cache to speed up builds significantly. Every command in Dockerfile is building in another docker container, and its results are stored in a separate layer. Layers are built on top of each other.
Docker scans Dockerfile and try to execute each steps one after another, before executing it probes if this layer is already in cache. When a cache is hit, building step is skipped, and from the user perspective is almost instant.
When you build your Dockerfile in a way that the most changing things such as application source code are on the bottom, you will experience instant builds.
Another way of amazingly fast building docker images is using a good base image – which you specify inFROM command, you can then only make necessary changes, not rebuild everything from scratch. This way, the build will be quicker. It’s especially beneficial if you have a host without the cache like Continuous Integration server.
Summing up, building Docker images with Dockerfile is faster than provisioning with Ansible, because of using docker cache and good base images. Moreover, you eliminate provisioning, by using ready to use configured images such stgresus.
$ docker run --name some-postgres -d postgres No installing postgres at all - it's ready to run. 
Also, you mention that docker allows multiple apps to run on one server.
It depends on your use case. You probably should split different components into separate containers. It will give you more flexibility.
Docker is very lightweight and running containers is cheap, especially if you store them in RAM – it’s possible to spawn new container for every http callback, however, it’s not very practical.
At work, I develop using a set of five different types of containers linked together.
In production some of them are replaced by real machines or even clusters of machine – however, settings on application level don’t change.
It’s possible because everything is communicating over the network. When you specify links in dockerrun command – docker bridges containers and injects environment variables with information about IPs and ports of linked children into the parent container.
This way, in my app settings file, I can read those values from the environment. In python it would be:
importosVARIABLE=os.environ.get('VARIABLE')
There is a tool which greatly simplifies working with docker containers, linking included. It’s called fig, and you can read more about it here.
Finally, what does the deploy process look like for dockerized apps stored in a git repo?
It depends on how your production environment looks like.
Example deploy process may look like this:
Build an app using docker build . in the code directory.
Test an image.
Push the new image out to registrydocker push myorg/myimage.
Notify remote app server to pull image from registry and run it (you can also do it directly using some configuration management tool).
Swap ports in a http proxy.
Stop the old container.
You can consider using amazon elastic beanstalk with docker or dokku.
Elastic beanstalk is a powerful beast and will do most of the deployment for you and provide features such as auto-scaling, rolling updates, zero deployment deployments and more.
Dokku is a very simple platform as a service similar to heroku.
42.What is a Docker container and how is it different than a VM?  Does containerization replace my virtualization infrastructure?
Containerization is very different from virtualization. It starts with the Docker engine, the tool that creates and runs containers (1 or more), and is the Docker installed software on any physical, virtual or cloud host with a compatible OS. Containerization leverages the kernel within the host operating system to run multiple root file systems. We call these root file systems “containers.” Each container shares the kernel within the host OS, allowing you to run multiple Docker containers on the same host. Unlike VMs, containers do not have an OS within it. They simply share the underlying kernel with the other containers. Each container running on a host is completely isolated so applications running on the same host are unaware of each other (you can use Docker Networking to create a multi-host overlay network that enables containers running on hosts to speak to one another).
The image below shows containerization on the left and virtualization on the right. Notice how containerization (left), unlike virtualization (right) does not require a hypervisor or multiple OSs.
Docker containers and traditional VMs are not mutually exclusive, so no, containers do not have to replace VMs. Docker containers can actually run within VMs. This allows teams to containerize each service and run multiple Docker containers per vm.
44.From an infrastructure standpoint, what do I need from Docker? Is Docker a piece of hardware running in my datacenter, and how taxing is it on my environment?
The Docker engine is the software that is installed on the host (bare metal server, VM or public cloud instance) and is the only “Docker infrastructure” you’ll need. The tool creates, runs and manages Docker containers. So actually, there is no hardware installation necessary at all.
The Docker Engine itself is very lightweight, weighing in around 80 MB total.
45.What exactly do you mean by “Dockerized node”? Can this node be on-premises or in the cloud?
A Dockerized node is anything i.e a bare metal server, VM or public cloud instance that has the Docker Engine installed and running on it.
Docker can manage nodes that exist on-premises as well as in the cloud. Docker Datacenter is an on-premises solution that enterprises use to create, manage, deploy and scale their applications and comes with support from the Docker team. It can manage hosts that exist in your datacenter as well as in your virtual private cloud or public cloud provider (AWS, Azure, Digital Ocean, SoftLayer etc.).
46.Do Docker containers package up the entire OS and make it easier to deploy?
Docker containers do not package up the OS. They package up the applications with everything that the application needs to run. The engine is installed on top of the OS running on a host. Containers share the OS kernel allowing a single host to run multiple containers.
47.What OS can the Docker Engine run on?
The Docker Engine runs on all modern Linux distributions. We also provide a commercially supported Docker Engine for Ubuntu, CentOS, OpenSUSE, RHEL. There is also a technical preview of Docker running on Windows Server 2016.

48.How does Docker help manage my infrastructure? Do I containerize all my infrastructure or something?
Docker isn’t focused on managing your infrastructure. The platform, which is infrastructure agnostic, manages your applications and helps ensure that they can run smoothly, regardless of infrastructure type via solutions like Docker Datacenter. This gives your company the agility, portability and control you require. Your team is responsible for managing the actual infrastructure.
49.How many containers can run per host?
As far as the number of containers that can be run, this really depends on your environment. The size of your applications as well as the amount of available resources (i.e like CPU) will all affect the number of containers that can be run in your environment. Containers unfortunately are not magical. They can’t create new CPU from scratch. They do, however, provide a more efficient way of utilizing your resources. The containers themselves are super lightweight (remember, shared OS vs individual OS per container) and only last as long as the process they are running. Immutable infrastructure if you will.
50.What do I have to do to begin the “Dockerization process”
The best way for your team to get started is for your developers to download Docker for Mac or Docker Windows. These are native installations of Docker on a Mac or Windows device. From their, developers will take their applications and create a Dockerfile. The Dockerfile is where all of the application configuration is specified. It is essentially the blueprint for the Docker Image. The image is a snapshot of your application and is what the Docker Engine looks at so it knows what the container it is spinning up should look like.
51.We have several monolithic applications in our environment. But Docker only works for microservices right?
I added this in because this is one of the biggest misconceptions about Docker. Docker can absolutely be used for to containerize monolithic apps as well as microservices based apps. We find that most customers who are leveraging Docker containerize their legacy monolithic applications to benefit from the isolation that Docker containers provide, as well as portability. Remember Docker containers can package up any application (monolithic or distributed) and migrate workloads to any infrastructure. This portability is what enables our enterprise customers to embrace strategies like moving to the hybrid cloud.
In the case of microservices, customers typically containerize each service and use tools like Docker Compose to deploy these multi-container distributed applications into their production environment as a single running application.
We’ve even seen some companies have a hybrid environment where they are slowly restructuring their dockerized monolithic applications to become dockerized distributed applications over time.
DOCKER FOR ME
Building Blocks:
Namespace:  Resource Allocation
cgroups:  Resource Limitation

Docker – Containerized application
Hosting:
Docker Cloud– Deployableenvironment for images with its reqd. runtime bins, libs, dependencies along with cloud infrastructure.
Docker Registry – A service responsible for hosting and distributing images.
Docker Hub – Arepository for all images of cloud either public or private.
Workstation:
Docker machine –  It is actual service 
To virtualize HOST OS.
Create virtual environment for Docker installation with docker engine.
Ability to connect to that virtual environment.
Run docker commands.
Docker Engine – It is used for building Docker images and creating Docker containers.
Docker Daemon(Server) – It is used to communicate and fetch images from Docker Hub.
( commanddockerd)
REST API– which specifies interfaces that programs can use to talk to the daemon and instruct it what to do.
Docker Client – Interactive terminal for command I/O (command docker)
Docker Compose - This is used to define applications using multiple Docker containers.
Docker Swarm – Clustering service/API & orchestrating containers in Docker.
How Docker works?

References: https://docs.docker.com/engine/docker-overview/
To generate this message, Docker took the following steps:                        
The Docker client contacted the Docker daemon.                                
The Docker daemon pulled the "hello-world" image from the Docker Hub. (amd64)(dockerd)
$ docker pull hello-world:latest
The Docker daemon created a new container from that image which runs executable that produces output
you are currently reading.                
$ docker run -t hello-world:latest
The Docker daemon streamed that output to the Docker client, which sent it to your terminal.

Docker Commands
In Docker 18.03.0-ce,
To stop container
docker container stop container_id
docker container restart container_id
docker ps --filter "status=exited" #show stopped containers





Docker Server and Client Application:
Docker Client 
Docker Server/ Docker Enginer/Daemon



Images:
Building blocks of Docker world.
Containers launched from images
Build:  Add file, Run Command, Open port. [ARO]
Registry:
Public – Docker Hub, Private – On Machine.
Containers (Instance of Image)
Launched from images
Images: Building aspect, Containers : Execution Aspect
Docker Container is
Image format
Set of Standard operations
Execution environment
One can’t run cross platform container on other. No windows container on Linux container.
 Containers provide way to virtualize OS in order for multiple workloads run on single OS instance.

 

Golden Image aka Preconfigured Image: 
Images expanding in irregular manner, update, image state vs running state. Update means even small change requires full image rebuild.
After updation, changes are not immediate you need to reboot each machine to see image change.
Docker engine is a program that builds containers from code. Also a service that distributes containers.



