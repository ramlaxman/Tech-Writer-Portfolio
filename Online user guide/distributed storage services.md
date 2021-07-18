What is Storage?
Most devices and applications read and/or write data. Here are some examples:
Buying a movie ticket online
Looking up the price of an online item
Taking a picture
Sending an email
Leaving a voicemail
In all of these cases, data is either read (looking up a price) or written (taking a picture). The type of data and how it's stored can be different in each of these cases.
Cloud providers typically offer services that can handle all of these types of data. For example, if you wanted to store text or a movie clip, you could use a file on disk. If you had a set of relationships such as an address book, you could take a more structured approach like using a database.
The advantage to using cloud-based data storage is you can scale to meet your needs. If you find that you need more space to store your movie clips, you can pay a little more and add to your available space. In some cases, the storage can even expand and contract automatically - so you pay for exactly what you need at any given point in time.

Types of Storages
Storage is found in many parts of the OpenStack cloud environment. It is important to understand the distinction between ephemeral storage and persistent storage:
Ephemeral storage - If you only deploy OpenStack Compute service (nova), by default your users do not have access to any form of persistent storage. The disks associated with VMs are ephemeral, meaning that from the user’s point of view they disappear when a virtual machine is terminated.
Persistent storage - Persistent storage means that the storage resource outlives any other resource and is always available, regardless of the state of a running instance.
OpenStack clouds explicitly support three types of persistent storage: Object Storage, Block Storage, and File-based storage.








Object storage:
Object storage manages data and links it to associated metadata.


Stored in flat namespace and retrieved by metadata or key knowledge.
Object = File + Metadata +key
File : samp.jpg
Metadata: image size, date created, category, state, city
Metadata: 
Describes object
Stored with object in extend attrib
Changed or modified
Indexed


Accessing
Parallelization to make million devices to fetch data
Requests for objects made via HTTP using REST API
Good for unstructured data
Able to give multi-tenancy for several kinds of workload and data on single system.
High scalability compared to block and file.
Multipetabyte installation is common.
No need to use compression and encryption traditional methods.
Flash memory for metadata only and 
Components of request:
HTTP action (GET, PUT, UPDATE, DELETE)
Authenticate Information
Storage URL
Optional: Metadata

-     An object is a piece of data paired with any associated metadata that provides context about the bytes contained within the object (things like how old or big the data is). Those 2 things—the data and metadata together—make an object.
-     Users access binary objects through a REST API. If your intended users need to archive or manage large datasets, you should provide them with Object Storage service.
-     Object storage, also known as object-based storage, is a flat structure in which files are broken into pieces and spread out among hardware. In object storage, the data is broken into discrete units called objects and is kept in a single repository, instead of being kept as files in folders or as blocks on servers.
Object storage volumes work as modular units: each is a self-contained repository that owns the data, a unique identifier that allows the object to be found over a distributed system, and the metadata that describes the data. That metadata is important and includes details like age, privacies/securities, and access contingencies. 
The data stored in objects is uncompressed and unencrypted, and the objects themselves are arranged in object stores (a central repository filled with many other objects) or containers (a package that contains all of the files an application needs to run).
Objects, object stores, and containers are very flat in nature—compared to the hierarchical structure of file storage systems—which allow them to be accessed very quickly at huge scale.
Object storage metadata can also be extremely detailed, and is capable of storing information on where a video was shot, what camera was used, and what actors are featured in each frame. To retrieve the data, the storage operating system uses the metadata and identifiers, which distributes the load better and lets administrators apply policies that perform more robust searches.
Object storage requires a simple HTTP application programming interface (API), which is used by most clients in all languages. 
Object storage is cost efficient: you only pay for what you use. It can scale easily, making it a great choice for public cloud storage. It’s a storage system well suited for static data, and its agility and flat nature means it can scale to extremely large quantities of data. The objects have enough information for an application to find the data quickly and are good at storing unstructured data.
Object storage and containers go hand-in-hand: Containers migrate from bare-metal environments to virtual machines and private clouds to public clouds far too often for most storage systems to keep up.
Traditional storage is difficult to port and file storage becomes onerous to navigate at the petabyte level, but objects contain just enough information for an application to find quickly and are free enough to store unstructured data like images and text files.

Additional benefits include:
OpenStack can store your virtual machine (VM) images inside of an Object Storage system, as an alternative to storing the images on a file system.
Integration with OpenStack Identity, and works with the OpenStack Dashboard.
Better support for distributed deployments across multiple datacenters through support for asynchronous eventual consistency replication.
Use if you need to:
eventually plan on distributing your storage cluster across multiple data centers.
unify accounts for your users for both compute and object storage.
control your object storage with the OpenStack Dashboard.

There are drawbacks, to be sure:
Objects can’t be modified — you have to write the object completely at once. 
Object storage also doesn’t work well with traditional databases, because writing objects is a slow process and writing an app to use an object storage API isn’t as simple as using file storage.
One can’t access it without HTTP RESTful method.
	
	Object Storage organizes data into containers of flexible sizes, with the individual pieces of data referred to as ‘objects’. The object will be a file like a photo or a video etc.
 
The objects are stored and managed in a flat organization of flexibly sized containers called ‘buckets’ or ‘containers’. ‘Buckets’ and ‘containers’ mean the same thing, it depends on the particular platform you're using which terminology is used.

Object Storage Scalability
 
The servers which make up the Object Storage platform are known as nodes. Each node has its own processor, memory and internal or external disks. A single node could be used but Object Storage systems are designed for scalability and in practice there will be multiple nodes.
 
The same bucket can span multiple nodes which can be spread across multiple geographic locations. This is a big difference between Object Storage and SAN and NAS. Object based storage architectures can be scaled out and managed simply by adding additional nodes in any location. It can grow out to massive sizes, and performance is not negatively impacted as it gets bigger.
 
Object Storage is very commonly offered by cloud providers. The best known example is S3 from Amazon Web Services. On premises and hybrid solutions are also available.
 
A hybrid solution is a platform that supports on premises nodes that can also store data on a cloud provider's Object Storage as well. Data can be replicated across both on premises and cloud locations.

Object Storage Attributes
 
Each object contains three things -the actual data itself (like a photo or video), customizable metadata, and a globally unique identifier.
Object Storage Metadata
 
Block storage doesn't keep metadata (that would be managed at the higher level of the operating system), and on NAS storage the metadata is fixed. With Object Storage the metadata is fully customizable, so you can add your own custom attributes. It links directly with the object and contains additional descriptive properties. This provides better indexing and management capabilities.
 
For example, we could add custom metadata to a photo that says ‘black’ and ‘cat’. This information is indexed and searchable. The search options are fully flexible and not limited to the filename, path and fixed metadata.
 
Another example would be for the medical industry. If you are uploading x-rays about a particular patient, the metadata could include the patient's name and the injury type.
 
You could also include all the useful information in a file name if you were using NAS, but file names would get crazy long and it wouldn’t be practical to manage. It would be very unwieldy and really just wouldn't work. Object Storage offers the most flexible and scalable indexing and search when you've got a large amount of unstructured data.
 
The customizable metadata also provides better management. You could for example set replication instructions through metadata, where different tags indicate how many copies of a particular object should be stored and where. Different objects can have different replication policies depending on their value.
 
Another example of customisable metadata providing enhanced, flexible management is control of storage tiering. Individual objects can be stored in different classes of storage depending on a metadata tag, for example ‘gold’ objects are stored on SSD and ‘bronze’ objects are stored on SATA drives. The policy can move objects to lower performance storage or delete them as they age, and it can be updated anytime as requirements change.
Globally Unique Identifier
 
A globally unique identifier is used rather than a file name and path as in NAS protocols. As the name suggests, the globally unique identifier is unique across the entire namespace and is used to find the object over the distributed system without having to know the physical location of the data. That removes the complexity and scalability challenges of a NAS hierarchical file system, which is based on complex file paths.
Data Protection – Replication and Erasure Coding
 
Object Storage provides resiliency through replication and/or erasure coding.
 
Replication is used to store multiple copies of objects on different nodes which can be in the same or different data centers. The object is still available on node failure because there are copies on multiple nodes. This is very suitable for small objects but not so good for very large ones. Having multiple copies of very large objects would take up a lot of space which would add to costs.
 
A suitable data protection option for very large objects is erasure coding. With erasure coding the object is broken up into smaller distributed parts. Parity information allows the data to be reconstructed if there is a node failure. It’s kind of similar to raid, but we’re striping an object across nodes rather than data across a set of disks. Because parity information is included the object can be reconstructed if there is node failure.
 
With replication multiple copies of the same object are stored in multiple nodes. With erasure encoding a single object is broken up into multiple parts which are spread across multiple nodes.
 
Traditional offsite backups are not required with Object Storage because offsite copies are built in as long as replication and/or erasure coding are configured. If there is a failure the data is still available and this is transparent to users and applications, they still get their data as if nothing had happened.
File Locking and In Place Edits are Not Supported
 
The way that Object Storage works when changes are made is different to how it works with a NAS file system. Object Storage does not typically support file locking, and files can't be updated in place. It was deliberately designed like this to make simple data protection replication and erasure coding possible.
 
Up to this point you maybe thought "everything is great about Object Storage. Why would I even use NAS anymore? Why don't we just use Object Storage for everything?" Well, Object Storage is not suitable when you've got data that is going to be edited by lots of different people and you want to have an ongoing single master copy of that.
 
Let’s say you've got a Word document associated with a project being run by your company, and it gets edited by multiple people. You need to have a single master copy of that document. NAS file systems support file locking to make sure that there's one consistent copy. Multiple people can read the file at the same time, but only one person can ever edit it at a time to make sure the data remains consistent and there are no conflicts. The user saves the file when they are done making changes and then the next person who wants to make changes edits the same single copy of the file. With Object Storage it's different - it doesn't support file locking and in place editing. If you've got multiple users that are editing the file and making changes, what happens is you end up with multiple different copies of that object. If multiple users update the same object concurrently, the system will simply write different versions of the object. That would make managing the project documentation in our example very impractical, so it's not a good use case for Object Storage.
 
Object Storage is designed for puts and gets, not for data which will have multiple edits from multiple users such as transactional databases or office Word documents. This has traditionally made it more suitable for secondary data - backups and archives, rather than primary data.
Versioning
 
Object Storage supports versioning where the old version of an object can be automatically saved if it is changed. This provides some data protection - if somebody overwrites an object or edits it, it will automatically save the old version so you don't lose the original data.
Cost
 
Object Storage is typically used as secondary storage (backup and archive) where performance is not a priority. It's usually one of the lowest cost storage options from a cloud provider, again because it's not typically running on high performance hardware. You can have high performance Object Storage if you want to, but that's not appropriate for most use cases.
 
On premises Object Storage platforms can typically be bought as an appliance or software only. When you buy an appliance it includes the hardware with the software installed. When you buy software only you install it on your own hardware. You can install the software on low cost commodity server hardware.
Object Storage Protocols and APIs
 
Object Storage uses RESTful APIs, which means it's using HTTP style requests to GET, PUT, POST and DELETE data. HEAD requests metadata information about the object.
 
Applications often access Object Storage directly through the API (Application Programming Interface). There have been open standard APIs developed to help accelerate Object Storage use across the industry.
 
CDMI is the Cloud Data Management Interface and is controlled by the Storage Networking Industry Association (SNIA).
 
S3 Simple Storage Service is an Object Storage service that you can buy from Amazon Web Services, but the S3 APIs have also been made available publicly. There is support for the S3 API on on-premises Object Storage platforms from other vendors such as NetApp and Dell EMC. A benefit is that these platforms can then easily integrate with the AWS S3 service for hybrid storage.
 
The other API commonly used is OpenStack Swift. OpenStack is an open standard initiative for cloud services and Swift is its Object Storage component.
 
CDMI is not in common use now, S3 and OpenStack Swift are more prevalent. Both S3 and OpenStack Swift are typically supported on on-premises platforms.
End User Access and Cloud Gateways
 
As well as direct access from applications, end users can usually also access the storage directly via a web browser. A web interface is well suited for this because the APIs use web style commands. Storage browsing applications such as CyberDuck are also available for end user access.
 
Support for access via NAS protocols is typically also included. This functionality can either be built directly in to the platform by the vendor or it can be provided via a cloud gateway. Cloud gateways are a hardware appliance or a virtual machine which sits between the clients and the Object Storage and translates between them. The clients talk to the cloud gateway using standard NAS protocols like SMB or NFS, and then the cloud gateway converts that to Object Storage APIs on the other side (and vice versa for traffic in the other direction).
Object Storage Benefits Summary
 
Single namespace with almost infinite scale
Scales across multiple physical locations
Performance does not degrade with scale
Customizable metadata for better indexing and management
Supports data management functions such as replication at object-level granularity
Typically low cost
Object Storage Limitations
 
Lower cost is a benefit but also a drawback as it means lower performance. This means Object Storage is not suitable for databases or other applications which require high performance.
 
It doesn’t have locking and file sharing facilities, so it’s not suitable for data which may be accessed concurrently and changed by multiple users or applications.
Object Storage Use Cases
 
Object Storage is best suited as a massively scalable store for unstructured data.
 
It's well suited for file content in the cloud space, especially images and videos - think YouTube.
 
It can be used as an additional storage tier beyond transactional storage for inactive data or as archival storage. Your primary storage system provides the required performance, and then you can tier the data off to the Object Storage beyond the primary storage.
 
As Object Storage evolves it may become more suitable for primary data, but it’s not a normal use case now. Object Storage is newer than SAN and NAS so it will evolve over time and other use cases are likely to emerge.
Use Case Examples
 
Media – large repositories of unstructured photos and video
Medical – patient records
Oil and Gas - seismic data
Object Storage Platform Examples
Cloud Providers:
Amazon Web Services Simple Storage Service (S3)
Microsoft Azure Blob Storage
Proprietary:
Facebook Haystack
On-Premises/Hybrid:
NetApp StorageGRID





Scalability, availability, durability, Lower TCO, rich metadata, 
Geoclustre: define and operate storage clusters across local failure domains (zones) and sites/regions(physical locations).
Manageability: automation for consistent operation.

              Object storage use cases:
Web content store
Large file workflows
Doc sync and share
Backups and disaster recovery
Private Cloud




































Block Storage

Block storage chunks data into arbitrarily organized, evenly sized volumes.

Located close to server in same data centers. 
It is a form of network-attached storage (NAS).Storage in such is organised as blocks.
Organizes data in separate vol accessed by one or very few servers simultaneously.
Vol made up of local HDD presented in form of sector and layouts.
Communication over dedicated SAN
Access Protocols: FC, iSCSI 
Best for Containers, VM, Databases which requires low latency and High IOPS.

Fibre Channel Protocol (FCP) is the SCSI interface protocol utilising an underlying Fibre Channel connection. The Fibre Channel standards define a high-speed data transfer mechanism that can be used to connect workstations, mainframes, supercomputers, storage devices and displays. FCP addresses the need for very fast transfers of large volumes of information and could relieve system manufacturers from the burden of supporting the variety of channels and networks, as it provides one standard for networking, storage and data transfer.

iSCSI is n computing, iSCSI (/ˈaɪskʌzi/ (listen) EYE-skuz-ee) is an acronym for Internet Small Computer Systems Interface, an Internet Protocol (IP)-based storage networking standard for linking data storage facilities. It provides block-level access to storage devices by carrying SCSI commands over a TCP/IP network. iSCSI is used to facilitate data transfers over intranets and to manage storage over long distances. It can be used to transmit data over local area networks (LANs), wide area networks (WANs), or the Internet and can enable location-independent data storage and retrieval. The protocol allows clients (called initiators) to send SCSI commands (CDBs) to storage devices (targets) on remote servers. It is a storage area network (SAN) protocol, allowing organizations to consolidate storage into storage arrays while providing clients (such as database and web servers) with the illusion of locally attached SCSI disks.[1] It mainly competes with Fibre Channel, but unlike traditional Fibre Channel which usually requires dedicated cabling,[a] iSCSI can be run over long distances using existing network infrastructure.[2] iSCSI was pioneered by IBM and Cisco in 1998 and submitted as a draft standard in March 2000
[SCSI: Small Computer System Interface (SCSI, SKUZ-ee) is a set of standards for physically connecting and transferring data between computers and peripheral devices. The SCSI standards define commands, protocols, electrical, optical and logical interfaces.]

Block storage chops data into blocks—get it?—and stores them as separate pieces. A block is a sequence of bytes and the smallest addressable unit. The OS is the intermediary between the application that wants to access files and the underlying file system and block-level storage. 
The disk file system manages where (at what block address) your files are persisted on the underlying block-level storage. Each block of data is given a unique identifier, which allows a storage system to place the smaller pieces of data wherever is most convenient. That means that some data can be stored in a Linux environment and some can be stored in a Windows unit.
Block storage is often configured to decouple the data from the user’s environment and spread it across multiple environments that can better serve the data. And then, when data is requested, the underlying storage software reassembles the blocks of data from these environments and presents them back to the user. It is usually deployed in storage-area network (SAN) environments and must be tied to a functioning server.
Because block storage doesn’t rely on a single path to data—like file storage does—it can be retrieved quickly. Each block lives on its own and can be partitioned so it can be accessed in a different operating system, which gives the user complete freedom to configure their data. 
It’s an efficient and reliable way to store data and is easy to use and manage. It works well with enterprises performing big transactions and those that deploy huge databases, meaning the more data you need to store, the better off you’ll be with block storage.
Block storage is implemented in OpenStack by the Block Storage service (cinder) because these 
volumes are persistent, they can be detached from one instance and re-attached to another instance and the data remains intact.
The Block Storage service supports multiple back ends in the form of drivers. Your choice of a storage back end must be supported by a block storage driver.
Most block storage drivers allow the instance to have direct access to the underlying storage hardware’s block device. This helps increase the overall read/write IO. However, support for utilizing files as volumes is also well established, with full support for NFS, GlusterFS and others.
These drivers work a little differently than a traditional block storage driver. On an NFS or GlusterFS file system, a single file is created and then mapped as a virtual volume into the instance. 
This mapping and translation is similar to how OpenStack utilizes QEMU’s file-based virtual machines stored in /var/lib/nova/instances.


There are some downsides, though:
Block storage can be expensive. 
Unable to scale upto petabyes
It restricts scalability and cost in larger scenarios.
It has limited capability to handle metadata, which means it needs to be dealt with in the application or database level—adding another thing for a developer or systems administrator to worry about.








Block Storage
 
Block storage stores and manages data in blocks - that's why it's called ‘block storage’. The storage is accessed via low level protocols using SCSI and NVME commands.
 
SAN protocols (Fibre Channel, FCoE and iSCSI) provide block access over a network where the disks are not directly attached to the individual client. The experience for the user and applications using block storage is similar to using a local disk inside that actual computer.
 
The low level direct access to the data reduces overhead by minimizing abstraction layers. Higher level tasks such as multi-user access, sharing, locking, and security are not handled by the block level access protocol, instead they are managed by the client’s operating system.
Block Storage Metadata
 
Metadata is data about other data, such as file name, owner, creation date etc.
 
As mentioned earlier, there’s very little overhead with block storage. It keeps no storage side metadata, only the block address. The block is simply a chunk of data that has got no description, no association, and no owner.
Block Storage Use Cases
 
Block storage is considered the best solution for performance sensitive, transactional, and database oriented applications. Because there's very little overhead it provides the best performance of the available external storage types.
 
Block storage is mostly used for primary storage (not secondary storage like backup and archiving).
 
The storage is typically accessed frequently by the clients, and the storage system and clients are usually both located in the same physical location. Because performance is important, we don't want to have a lot of distance between them because that would add to the latency and harm performance.




























File Storage
File storage organizes and represents data as a hierarchy of files in folders




It is based on NAS
It is connected to LAN accessed by servers and clients like PC.
Communication protocols: SMB and NFS.
Good for high throughput, 
Non latency workloads where scalability is not the key.
Cost of maintenance is low compared to Block
Limited amount of memory is aimed at freq accessed data and metadata with large pool of HDD
Good for caching and automated tiering functionality




In multi-tenant OpenStack cloud environment, the Shared File Systems service (manila) provides a set of services for management of shared file systems. 
The Shared File Systems service supports multiple back-ends in the form of drivers, and can be configured to provision shares from one or more back-ends. 
Share servers are virtual machines that export file shares using different file system protocols such as NFS, CIFS, GlusterFS, or HDFS.
The Shared File Systems service is persistent storage and can be mounted to any number of client machines. It can also be detached from one instance and attached to another instance without data loss. During this process the data are safe unless the Shared File Systems service itself is changed or removed.
Users interact with the Shared File Systems service by mounting remote file systems on their instances with the following usage of those systems for file storing and exchange.
The Shared File Systems service provides shares which is a remote, mountable file system. You can mount a share and access a share from several hosts by several users at a time. 
With shares, you can also:
Create a share specifying its size, shared file system protocol, visibility level.
Create a share on either a share server or standalone, depending on the selected back-end mode, with or without using a share network.
Specify access rules and security services for existing shares.
Combine several shares in groups to keep data consistency inside the groups for the following safe group operations.
Create a snapshot of a selected share or a share group for storing the existing shares consistently or creating new shares from that snapshot in a consistent way.
Create a share from a snapshot.
Set rate limits and quotas for specific shares and snapshots.
View usage of share resources.
Remove shares. [part to be introduced in Ceph FS]

File storage, also called file-level or file-based storage, is exactly what you think it might be: Data is stored as a single piece of information inside a folder, just like you’d organize pieces of paper inside a manila folder. 
When you need to access that piece of data, your computer needs to know the path to find it. (Beware—It can be a long, winding path.) Data stored in files is organized and retrieved using a limited amount of metadata that tells the computer exactly where the file itself is kept. It’s like a library card catalog for data files.






Think of a closet full of file cabinets. Every document is arranged in some type of logical hierarchy—by cabinet, by drawer, by folder, then by piece of paper. This is where the term hierarchical storage comes from, and this is file storage. It is the oldest and most widely used data storage system for direct and network-attached storage systems, and it’s one that you’ve probably been using for decades. Any time you access documents saved in files on your personal computer, you use file storage. File storage has broad capabilities and can store just about anything. It’s great for storing an array of complex files and is fairly fast for users to navigate.
File Storage
 
NAS protocols (CIFS, SMB, and NFS) use file storage, which stores data as a file hierarchy in a file system - that's why it's called ‘file storage’. The hierarchy is similar to a physical file cabinet like you would find in an office with folders (also known as directories) and sub-folders (also known as sub-directories).
 
The user or application connects to the file system through a share if it’s CIFS/SMB, or by mounting an export with NFS. CIFS/SMB is typically used by Windows clients and NFS by Unix and Linux clients, but all the protocols are supported by the different clients.
File Storage Metadata
 
File system metadata is recorded separately from the file itself and records basic file attributes such as the file name, the creation date, who the creator is, the file type (such as PDF or Word document), the most recent change, and when it was last accessed.
 
The metadata is fixed and standardized to that particular file system.
 
To add custom metadata (known as ‘extended attributes’) you or the vendor has to build a custom application and database. That adds a lot of complexity and is not commonly done.
File Storage Use Cases
 
File storage is well suited to general purpose data, especially data which is edited frequently and data which is concurrently accessed by multiple users or applications. For example a shared Word document that is getting constantly updated by different people.
 
It's designed to be accessed over both the local network and remotely. Performance is not typically as much a concern as it is for the SAN protocols, so it's common that users can access the data both in the same building and also over a wide area network.
Block and File Storage Limitations
 
Block and file storage systems can be scaled out by adding more disks or nodes, but they're typically limited in scale. There's a maximum size for a single system, and it's usually limited to a single geographic area. You can’t normally have it spread across multiple locations.
 
NAS file index tables (inodes) have a maximum size and can affect performance if they grow too large. Performance can be negatively impacted by scaling on NAS file systems.
 
SAN and NAS systems both need to be backed up offsite for resiliency because your storage system is in one physical location. If there is natural disaster like a flood or fire it would all be gone, so you need to back up the data to a separate physical location.


The problem is, just like with your filing cabinet, that virtual drawer can only open so far. File-based storage systems must scale out by adding more systems, rather than scale up by adding more capacity.










Comparison



Storage Architecture in Openstack

OpenStack has multiple storage realms to consider:
Object Storage (swift)
Block Storage (cinder)
Image storage (glance)
Ephemeral storage (nova)

Object Storage (swift)
The Object Storage (swift) service implements a highly available, distributed, eventually consistent object/blob store that is accessible via HTTP/HTTPS. The following diagram illustrates how data is accessed and replicated.


The swift-proxy service is accessed by clients via the load balancer on the management network (br-mgmt). The swift-proxy service communicates with the Account, Container, and Object services on the Object Storage hosts via the storage network(br-storage). Replication between the Object Storage hosts is done via the replication network (br-repl).
Block Storage (cinder)
The Block Storage (cinder) service manages volumes on storage devices in an environment. In a production environment, the device presents storage via a storage protocol (for example, NFS, iSCSI, or Ceph RBD) to a storage network (br-storage) and a storage management API to the management network (br-mgmt). Instances are connected to the volumes via the storage network by the hypervisor on the Compute host.
The following diagram illustrates how Block Storage is connected to instances.

The diagram shows the following steps.
1
A volume is created by the assigned cinder-volume service using the appropriate cinder driver. The volume is created by using an API that is presented to the management network.
2
After the volume is created, the nova-compute service connects the Compute host hypervisor to the volume via the storage network.
3
After the hypervisor is connected to the volume, it presents the volume as a local hardware device to the instance.

Important
The LVMVolumeDriver is designed as a reference driver implementation, which we do not recommend for production usage. The LVM storage back-end is a single-server solution that provides no high-availability options. If the server becomes unavailable, then all volumes managed by the cinder-volume service running on that server become unavailable. Upgrading the operating system packages (for example, kernel or iSCSI) on the server causes storage connectivity outages because the iSCSI service (or the host) restarts.
Because of a limitation with container iSCSI connectivity, you must deploy the cinder-volume service directly on a physical host (not into a container) when using storage back ends that connect via iSCSI. This includes the LVMVolumeDriver and many of the drivers for commercial storage devices.

Note
The cinder-volume service does not run in a highly available configuration. When the cinder-volume service is configured to manage volumes on the same back end from multiple hosts or containers, one service is scheduled to manage the life cycle of the volume until an alternative service is assigned to do so. This assignment can be made through the cinder-manage CLI tool. This configuration might change if cinder volume active-active support spec is implemented.
Image storage (glance)
The Image service (glance) can be configured to store images on a variety of storage back ends supported by the glance_store drivers.
Important
When the File System store is used, the Image service has no mechanism of its own to replicate the image between Image service hosts. We recommend using a shared storage back end (via a file system mount) to ensure that all glance-api services have access to all images. Doing so prevents losing access to images when an infrastructure (control plane) host is lost.
The following diagram illustrates the interactions between the Image service, the storage device, and the nova-compute service when an instance is created.



The diagram shows the following steps.
1
When a client requests an image, the glance-api service accesses the appropriate store on the storage device over the storage network (br-storage) and pulls it into its cache. When the same image is requested again, it is given to the client directly from the cache.
2
When an instance is scheduled for creation on a Compute host, the nova-compute service requests the image from the glance-api service over the management network (br-mgmt).
3
After the image is retrieved, the nova-compute service stores the image in its own image cache. When another instance is created with the same image, the image is retrieved from the local base image cache.

Ephemeral storage (nova)¶
When the flavors in the Compute service are configured to provide instances with root or ephemeral disks, the nova-compute service manages these allocations using its ephemeral disk storage location.
In many environments, the ephemeral disks are stored on the Compute host’s local disks, but for production environments we recommend that the Compute hosts be configured to use a shared storage subsystem instead. A shared storage subsystem allows quick, live instance migration between Compute hosts, which is useful when the administrator needs to perform maintenance on the Compute host and wants to evacuate it. Using a shared storage subsystem also allows the recovery of instances when a Compute host goes offline. The administrator is able to evacuate the instance to another Compute host and boot it up again. The following diagram illustrates the interactions between the storage device, the Compute host, the hypervisor, and the instance.






The diagram shows the following steps.
1
The Compute host is configured with access to the storage device. The Compute host accesses the storage space via the storage network (br-storage) by using a storage protocol (for example, NFS, iSCSI, or Ceph RBD).
2
The nova-compute service configures the hypervisor to present the allocated instance disk as a device to the instance.
3
The hypervisor presents the disk as a device to the instance.


Commodity storage technologies
There are various commodity storage back end technologies available. Depending on your cloud user’s needs, you can implement one or many of these technologies in different combinations.
Ceph
Ceph is a scalable storage solution that replicates data across commodity storage nodes.
Ceph utilises and object storage mechanism for data storage and exposes the data via different types of storage interfaces to the end user it supports interfaces for: - Object storage - Block storage - File-system interfaces
Ceph provides support for the same Object Storage API as swift and can be used as a back end for the Block Storage service (cinder) as well as back-end storage for glance images.
Ceph supports thin provisioning implemented using copy-on-write. This can be useful when booting from volume because a new volume can be provisioned very quickly. Ceph also supports keystone-based authentication (as of version 0.56), so it can be a seamless swap in for the default OpenStack swift implementation.
Ceph’s advantages include:
The administrator has more fine-grained control over data distribution and replication strategies.
Consolidation of object storage and block storage.
Fast provisioning of boot-from-volume instances using thin provisioning.
Support for the distributed file-system interface CephFS.
You should consider Ceph if you want to manage your object and block storage within a single system, or if you want to support fast boot-from-volume.
Gluster
A distributed shared file system. As of Gluster version 3.3, you can use Gluster to consolidate your object storage and file storage into one unified file and object storage solution, which is called Gluster For OpenStack (GFO). GFO uses a customized version of swift that enables Gluster to be used as the back-end storage.
The main reason to use GFO rather than swift is if you also want to support a distributed file system, either to support shared storage live migration or to provide it as a separate service to your end users. If you want to manage your object and file storage within a single system, you should consider GFO.
LVM
The Logical Volume Manager (LVM) is a Linux-based system that provides an abstraction layer on top of physical disks to expose logical volumes to the operating system. The LVM back-end implements block storage as LVM logical partitions.
On each host that will house block storage, an administrator must initially create a volume group dedicated to Block Storage volumes. Blocks are created from LVM logical volumes.
 
Note
LVM does not provide any replication. Typically, administrators configure RAID on nodes that use LVM as block storage to protect against failures of individual hard drives. However, RAID does not protect against a failure of the entire host.
iSCSI¶
Internet Small Computer Systems Interface (iSCSI) is a network protocol that operates on top of the Transport Control Protocol (TCP) for linking data storage devices. It transports data between an iSCSI initiator on a server and iSCSI target on a storage device.
iSCSI is suitable for cloud environments with Block Storage service to support applications or for file sharing systems. Network connectivity can be achieved at a lower cost compared to other storage back end technologies since iSCSI does not require host bus adaptors (HBA) or storage-specific network devices.
NFS¶
Network File System (NFS) is a file system protocol that allows a user or administrator to mount a file system on a server. File clients can access mounted file systems through Remote Procedure Calls (RPC).
The benefits of NFS is low implementation cost due to shared NICs and traditional network components, and a simpler configuration and setup process.
For more information on configuring Block Storage to use NFS storage, see Configure an NFS storage back end in the OpenStack Administrator Guide.
Sheepdog
Sheepdog is a userspace distributed storage system. Sheepdog scales to several hundred nodes, and has powerful virtual disk management features like snapshot, cloning, rollback and thin provisioning.
It is essentially an object storage system that manages disks and aggregates the space and performance of disks linearly in hyper scale on commodity hardware in a smart way. On top of its object store, Sheepdog provides elastic volume service and http service. Sheepdog does require a specific kernel version and can work nicely with xattr-supported file systems.
ZFS
The Solaris iSCSI driver for OpenStack Block Storage implements blocks as ZFS entities. ZFS is a file system that also has the functionality of a volume manager. This is unlike on a Linux system, where there is a separation of volume manager (LVM) and file system (such as, ext3, ext4, xfs, and btrfs). ZFS has a number of advantages over ext4, including improved data-integrity checking.
The ZFS back end for OpenStack Block Storage supports only Solaris-based systems, such as Illumos. While there is a Linux port of ZFS, it is not included in any of the standard Linux distributions, and it has not been tested with OpenStack Block Storage. As with LVM, ZFS does not provide replication across hosts on its own, you need to add a replication solution on top of ZFS if your cloud needs to be able to handle storage-node failures.


<()