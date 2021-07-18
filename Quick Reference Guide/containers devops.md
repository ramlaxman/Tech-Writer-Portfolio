Containers
Who: 

Solomon Hykes

http://rhelblog.redhat.com/2015/08/28/the-history-of-containers/
What : 
 Operating-system-level virtualization is a server virtualization method in which the kernel of an operating system allows the existence of multiple isolated user-space instances, instead of just one. Such instances, which are sometimes called containers, software containers, virtualization engines (VEs) or jails (FreeBSD jail or chroot jail), may look and feel like a real server from the point of view of its owners and users.



How are they different?

a server running three containerized applications as with Docker runs a single operating system, and each container shares the operating system kernel with the other containers. Shared parts of the operating system are read only, while each container has its own mount (i.e., a way to access the container) for writing. That means the containers are much more lightweight and use far fewer resources than virtual machines.

Containers vs VMs: Which is better in the Data Center?

The determination of which is better in Containers vs VMs is dependent on what you are trying to accomplish.  Virtualization enables workloads to be run in environments that are separated from their underlying hardware by a layer of abstraction. This abstraction allows servers to be broken up into virtualized machines (VMs) that can run different operating systems.
Container technology offers an alternative method for virtualization, in which a single operating system on a host can run many different applications from the cloud. One way to think of containers vs VMs is that while VMs run several different operating systems on one compute node, container technology offers the opportunity to virtualize the operating system itself.
Containers vs VMs:  Virtual Machine Workloads
A  VM is a software-based environment geared to simulate a hardware-based environment, for the sake of the applications it will host. Conventional applications are designed to be managed by an operating system and executed by a set of processor cores. Such applications can run within a VM without any re-architecture.
With VMs, a software component called a hypervisor acts as an agent between the VM environment and the underlying hardware, providing the necessary layer of abstraction. A hypervisor, such as VMware ESXi, is responsible for executing the virtual machine assigned to it and can execute several simultaneously. Other popular hypervisors include KVM, Citrix Xen, and Microsoft Hyper-V. In the most recent VM environments, modern processors are capable of interacting with hypervisors directly, providing them with channels for pipelining instructions from the VM in a manner that is completely opaque to the applications running inside the VM. They also include sophisticated network virtualization models such as VMware NSX.
The scalability of a VM server workload is achieved in much the same way it is achieved on bare metal: With a Web server or a database server, the programs responsible for delivering service are distributed among multiple hosts. Load balancers are inserted in front of those hosts to direct traffic among them equably. Automated procedures within VM environments make such load balancing processes sensitive to changes in traffic patterns across data centers.
Containers vs VMs:  Container-Driven Workloads
The concept of containerization was originally developed, not as an alternative to VM environments, but as a way to segregate namespaces in a Linux operating system for security purposes. The first Linux environments, resembling modern container systems, produced partitions (sometimes called “jails”) within which applications of questionable security or authenticity could be executed without risk to the kernel. The kernel was still responsible for execution, though a layer of abstraction was inserted between the kernel and the workload.
Once the environment within these partitions was minimized for efficiency’s sake, the idea of making the contents of these partitions portable came later. The first true container system was not yet an environment: LXC, developed as a part of Linux. Docker originated as an experiment for easily deploying LXC containers onto a PaaS platform operated by Docker Inc.’s original parent company, dotCloud.
Workloads within containers such as Docker are virtualized. However, within Docker’s native environment, there is no hypervisor (see Figure 1). Instead, the Linux kernel (or, more recently, the Windows Server kernel) is supplemented by a daemon that maintains the compartmentalization between containers, while connecting their workloads to the kernel. Modern containers often do include minimalized operating systems such as CoreOS and VMware’s Photon OS – their only purpose is to maintain basic, local services for the programs they host, not to project the image of a complete processor space.

Figure 1. Containers vs Virtual Machines, courtesy of Docker Inc. and RightScale Inc.

In the architecture first employed at Google and at streaming video service provider Netflix, microservices are functions that can operate without exclusivity to any single application. They perform small workloads, in the form of functions that can be contacted via APIs and that produce discrete outputs. Such functions exist in traditional, monolithic applications today, although multiple applications instantiate these same functions redundantly. In a microservices architecture, these functions are more like libraries, providing service to any and all applications that require them.
Scalability of containerized workloads is a completely different process from VM workloads. Modern containers include only the basic services their functions require, but one of them is a Web server, such as NGINX, that also acts as a load balancer. An orchestration system such as Google Kubernetes or Mesosphere Marathon is capable of determining, based upon traffic patterns, when the quantity of containers needs to scale out, can replicate container images automatically, and can then remove them from the system.
The key characteristic distinguishing a container from a VM is the container’s ephemeral nature. In a modern orchestration system, multiple copies of a container coexist. Containers that fail can be removed and replaced without noticeable impact on service. In the most radical environments, where continuous delivery methods are in place, new or experimental versions of containers may coexist with older versions. If an experiment fails, all the newer versions can be rolled back and replaced. These new and vastly different methods of managing data centers are key to the overwhelming interest the telecom industry has displayed in Docker and its associated technologies, in the handful of months they have existed.






How do containers work?

http://www.networkworld.com/article/2226996/cisco-subnet/software-containers--used-more-frequently-than-most-realize.html
https://www.youtube.com/watch?v=YsYzMPptB-k
http://www.informationweek.com/strategic-cio/it-strategy/containers-explained-9-essentials-you-need-to-know/a/d-id/1318961


When are they required?
http://cloudacademy.com/blog/container-virtualization/




Advantages & Disadvantages:
https://people.hofstra.edu/geotrans/eng/ch3en/conc3en/table_advantageschallengescont.html
http://searchservervirtualization.techtarget.com/definition/container-based-virtualization-operating-system-level-virtualization



-----------------------------------------------------------
Resources:
http://rhelblog.redhat.com/2015/08/28/the-history-of-containers/
https://www.sdxcentral.com/cloud/containers/definitions/what-are-containers-like-docker-linux-containers/
https://www.sdxcentral.com/cloud/containers/definitions/containers-vs-vms/
http://www.computerweekly.com/feature/What-are-containers-and-microservices
http://www.cio.com/article/2924995/enterprise-software/what-are-containers-and-why-do-you-need-them.html
http://searchservervirtualization.techtarget.com/definition/hosted-hypervisor-Type-2-hypervisor










Docker Invocation
Jacques - Multiple servers on single system
Paul – Cgroups [Control Group of process of CPU, memory]
Tejun – Massive redesign of containers namespaces introduced [Container can only see & access its resources like CPU, Memory, Storage,  I/O or all at once ]
Pros
-          Instance of guest OS image if it is OS container.
-          OS virtualization use hardware virtualization for creating ISO related environments similar like 
namespaces.
-          Uses OS and CPU directly
-          Host OS sufficient
-          On Linux machine itself
-          Not using whole OS
-          Not any 3rd Party like hyper-v.
-          Lightweight
-          Mostly OS board: Hyper-V: Microsoft, QEMU, KVM: Linux.
Cons
-          Frequent environment changes
-          Application deploy specific
-          Less workload.
-          Not for all
-          In case cross platform, fail for performance.
-          Weaker Isolation
-          Depedenancy

Solomon Hykes 2014
-          SOFTWARE ARCHITECTURE standards.
-          Directly with OS
-          Layer of security and cross platform..
-          Uses OS virtualization
-          Xen  is hypervisor
-          Use boot2docker. Iso to start docker client
-          Portability
-          Server like environment on one’s laptop (entryl link)
-          Community and enterprise images on Docker Hub.
-          Network between Containers is tedious process.
-          Docker on Cross platform
-          Backward Compatible
-          What if one contain build using docker and while other like using rkt.











