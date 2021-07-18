User Based Commands:

[root@Cloud Downloads]#  euca-describe-instances

RESERVATION	r-A8CE3FD4	077577678152	For_Linux
INSTANCE	i-A7F240F7	emi-44E3420F			stopped	admin	0  m1.medium 2014-01-24T11:17:27.857Z	clearlogy	monitoring-disabled	ebs	hvm


[root@Cloud Downloads]# euca-describe-availability-zones verbose

AVAILABILITYZONE	clearlogy	192.168.2.21 arn:euca:eucalyptus:clearlogy:cluster:clearlogy_cc/	
AVAILABILITYZONE	|- vm types	free / max   cpu   ram  disk	
AVAILABILITYZONE	|- m1.small	0005 / 0006   1    256     5	
AVAILABILITYZONE	|- t1.micro	0005 / 0006   1    256     5	
AVAILABILITYZONE	|- c1.medium	0004 / 0005   1    512    10	
AVAILABILITYZONE	|- m1.large	0002 / 0003   2    512    10	
AVAILABILITYZONE	|- m1.medium	0003 / 0003   1   1024    10	
AVAILABILITYZONE	|- m1.xlarge	0002 / 0003   2   1024    10	
AVAILABILITYZONE	|- c1.xlarge	0001 / 0001   2   2048    10	

Launch the Instance from user console.

For Linux,

Go to directory of admin.pem file.

[root@abc]# chmod 400 admin.pem

[root@abc]# ssh -i admin.pem root@192.168.77.22

For windows,

Launch Windows Instance
Now to ensure instance, wait for Instance status in User console.
Once instance is shown in Ready state, use one of the following procedure:

Now, use the VNC viewer 
in VNC viewer, 192.168.77.11::5900 and you will see Windows Instance running.

or Using rdesktop, 
[root@abc]#  rdesktop -u clearlogy1 192.168.77.23




Admin Based Commands
Perform All activities on CLC i.e. 192.168.77.10

First, we have to confirm that all services are running fine:
[root@localhost Downloads]# euca-describe-services 
SERVICE	storage        	clearlogy      	clearlogy_sc   	ENABLED   	22  	http://192.168.2.21:8773/services/Storage	arn:euca:eucalyptus:clearlogy:storage:clearlogy_sc/
SERVICE	bootstrap      	bootstrap      	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/Empyrean	arn:euca:bootstrap:::192.168.2.21/
SERVICE	walrus         	walrus         	walrus         	ENABLED   	22  	http://192.168.2.21:8773/services/Walrus	arn:euca:bootstrap:walrus:walrus:walrus/
SERVICE	cluster        	clearlogy      	clearlogy_cc   	ENABLED   	22  	http://192.168.2.21:8774/axis2/services/EucalyptusCC	arn:euca:eucalyptus:clearlogy:cluster:clearlogy_cc/
SERVICE	eucalyptus     	eucalyptus     	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/Eucalyptus	arn:euca:eucalyptus:::192.168.2.21/
SERVICE	reporting      	bootstrap      	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/Reporting	arn:euca:bootstrap::reporting:192.168.2.21/
SERVICE	autoscaling    	autoscaling    	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/AutoScaling	arn:euca:eucalyptus:autoscaling:autoscaling:192.168.2.21/
SERVICE	euare          	eucalyptus     	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/Euare 	arn:euca:eucalyptus::euare:192.168.2.21/
SERVICE	notifications  	eucalyptus     	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/Notifications	arn:euca:eucalyptus::notifications:192.168.2.21/
SERVICE	cloudwatch     	cloudwatch     	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/CloudWatch	arn:euca:eucalyptus:cloudwatch:cloudwatch:192.168.2.21/
SERVICE	tokens         	eucalyptus     	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/Tokens	arn:euca:eucalyptus::tokens:192.168.2.21/
SERVICE	dns            	eucalyptus     	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/Dns   	arn:euca:eucalyptus::dns:192.168.2.21/
SERVICE	jetty          	eucalyptus     	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/Jetty 	arn:euca:eucalyptus::jetty:192.168.2.21/
SERVICE	loadbalancing  	loadbalancing  	192.168.2.21   	ENABLED   	22  	http://192.168.2.21:8773/services/LoadBalancing	arn:euca:eucalyptus:loadbalancing:loadbalancing:192.168.2.21/

To get new credentials, in any case, use following procedure:

[root@localhost Documents]# euca_conf --get-credentials admin.zip

[root@localhost Documents]# unzip admin.zip
Archive:  admin.zip
To setup the environment run: source /path/to/eucarc
  inflating: eucarc                  
  inflating: iamrc                   
  inflating: cloud-cert.pem          
  inflating: jssecacerts             
  inflating: euca2-admin-7e1603ea-pk.pem  
  inflating: euca2-admin-7e1603ea-cert.pem  
[root@localhost Documents]# source eucarc

[root@localhost Documents]# euca-describe-nodes 

NODE	clearlogy		192.168.2.20	ENABLED	
INSTANCE	i-ACC03BFE
INSTANCE	i-6E1B41FB
INSTANCE	i-B5504588
INSTANCE	i-A7F240F7
INSTANCE	i-945D409D

To Restart Eucalyptus

The recommended processes to restart Eucalyptus, including terminating instances and restarting Eucalyptus components. You must restart Eucalyptus whenever you make a physical change (e.g., switch out routers), or edit the eucalyptus.conf file.

To restart Eucalyptus, perform the following tasks in the order presented.

Before you restart Eucalyptus, we recommend that you notify all users that you are terminating all instances.

a) Shut Down All Instances

[root@localhost Documents]# euca-terminate-instances i-6E1B41FB

INSTANCE	i-6E1B41FB	running	shutting-down

[root@localhost Documents]# euca-terminate-instances i-6E1B41FB

INSTANCE	i-6E1B41FB	terminated	terminated

b) On Node controller i.e. 192.168.77.11 & 12,

[root@localhost Documents]# service eucalyptus-nc stop

Repeat for each machine hosting an NC.

c) On CLC machine, 192.168.77.10, 
[root@localhost Documents]# service eucalyptus-cc cleanstop
[root@localhost Documents]# service eucalyptus-cloud stop
[root@localhost Documents]# service eucalyptus-cloud start
[root@localhost Documents]# service eucalyptus-cloud cleanstart

d) Now, On NC machines, 
[root@localhost Documents]# service eucalyptus-nc start

e) Wait for 1-2 minutes, now on CLC,
[root@localhost Downloads]# euca-describe-services 
and all service status will be displayed.
Tips:

1. If availability zones are 0000/0000, then

Do on NC & CLC machine,

[root@abc]# ntpdate -u 0.centos.pool.ntp.org
[root@abc Downloads]# source eucarc
[root@abc]# euca-describe-nodes

and then do 
[root@Cloud Downloads]# euca-describe-availability-zones verbose

2. If ssh message fails like this,

[root@localhost Downloads]# ssh -i admin.pem root@192.168.2.100

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that the RSA host key has just been changed.
The fingerprint for the RSA key sent by the remote host is 05:4e:85:6f:f7:83:74:36:f4:09:2b:92:86:35:d9:fe.
Please contact your system administrator. Add correct host key in /root/.ssh/known_hosts to get rid of this message.
Offending key in /root/.ssh/known_hosts:5.
RSA host key for 192.168.2.100 has changed and you have requested strict checking.
Host key verification failed.

Sol:  Go to /root/.ssh/known_hosts
         Remove the entry for particulcar IP address
         Again do the SSH & now it will work.

[root@localhost Downloads]# ssh -i admin.pem root@192.168.2.100
The authenticity of host '192.168.2.100 (192.168.2.100)' can't be established.
RSA key fingerprint is 05:4e:85:6f:f7:83:74:36:f4:09:2b:92:86:35:d9:fe.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.2.100' (RSA) to the list of known hosts.
[root@ip-10-10-1-153 ~]# 
