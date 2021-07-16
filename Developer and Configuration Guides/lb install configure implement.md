[root@localhost ~]# yum install eucalyptus-load-balancer-image

Loaded plugins: fastestmirror, refresh-packagekit, security
Loading mirror speeds from cached hostfile
epel/metalink                                                                                                                | 3.6 kB     00:00     
 * base: mirror.leapswitch.com
 * elrepo: ftp.nluug.nl
 * epel: epel.mirror.net.in
 * extras: mirror.leapswitch.com
 * updates: mirror.leapswitch.com
base                                                                                                                         | 3.7 kB     00:00     
elrepo                                                                                                                       | 2.9 kB     00:00     
epel                                                                                                                         | 4.2 kB     00:00     
epel/primary_db                                                                                                              | 5.8 MB     00:31     
euca2ools-release                                                                                                            | 1.2 kB     00:00     
eucalyptus-release                                                                                                           | 1.8 kB     00:00     
extras                                                                                                                       | 3.4 kB     00:00     
updates                                                                                                                      | 3.4 kB     00:00     
Setting up Install Process
Resolving Dependencies
--> Running transaction check
---> Package eucalyptus-load-balancer-image.x86_64 0:1.0.3-0.148.el6 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

====================================================================================================================================================
 Package                                         Arch                    Version                          Repository                           Size
====================================================================================================================================================
Installing:
 eucalyptus-load-balancer-image                  x86_64                  1.0.3-0.148.el6                  eucalyptus-release                  151 M

Transaction Summary
====================================================================================================================================================
Install       1 Package(s)

Total download size: 151 M
Installed size: 163 M
Is this ok [y/N]: y
Downloading Packages:
eucalyptus-load-balancer-image-1.0.3-0.148.el6.x86_64.rpm                                                                    | 151 MB     15:56     
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing : eucalyptus-load-balancer-image-1.0.3-0.148.el6.x86_64                                                                            1/1 
  Verifying  : eucalyptus-load-balancer-image-1.0.3-0.148.el6.x86_64                                                                            1/1 

Installed:
  eucalyptus-load-balancer-image.x86_64 0:1.0.3-0.148.el6                                                                                           

Complete!

Now to avoid security token error, delete old credentials & source new credentials from Admin console or from euca2ools.

[root@localhost Downloads]# source eucarc

[root@localhost Downloads]# euca-install-load-balancer --install-default
Installing default Load Balancer tarball.
Found tarball /usr/share/eucalyptus-load-balancer-image/eucalyptus-load-balancer-image-1.0.3-148.tgz
Preparing to extract image...
Extracting ramdisk 100% |======================================================================================|   5.77 MB 108.39 MB/s Time: 0:00:00
Bundling ramdisk   100% |======================================================================================|   5.77 MB  21.02 MB/s Time: 0:00:00
-- Uploading ramdisk image --
initramfs-2.6.32-358.23.2.el6.x86_64.img.part.0 100% |=========================================================|   5.74 MB  10.74 MB/s Time: 0:00:00
initramfs-2.6.32-358.23.2.el6.x86_64.img.manifest.xml 100% |===================================================|   3.38 kB  16.18 kB/s Time: 0:00:00
Registered ramdisk image eri-CF4937A3
Extracting kernel  100% |======================================================================================|   3.86 MB  46.58 MB/s Time: 0:00:00
Bundling kernel    100% |======================================================================================|   3.86 MB  18.77 MB/s Time: 0:00:00
-- Uploading kernel image --
vmlinuz-2.6.32-358.23.2.el6.x86_64.part.0 100% |===============================================================|   3.81 MB  15.57 MB/s Time: 0:00:00
vmlinuz-2.6.32-358.23.2.el6.x86_64.manifest.xml 100% |=========================================================|   3.42 kB  20.20 kB/s Time: 0:00:00
Registered kernel image eki-BB1F39FB
Extracting image   100% |======================================================================================| 682.00 MB 113.86 MB/s Time: 0:00:06
Bundling image     100% |======================================================================================| 682.00 MB  19.33 MB/s Time: 0:00:36
-- Uploading machine image --
eucalyptus-load-balancer-image-1.0.3-148.img.part.0  ( 1/16) 100% |============================================|  10.00 MB  29.83 MB/s Time: 0:00:00
eucalyptus-load-balancer-image-1.0.3-148.img.part.1  ( 2/16) 100% |============================================|  10.00 MB  35.37 MB/s Time: 0:00:00
.
.
.
.
.
eucalyptus-load-balancer-image-1.0.3-148.img.part.15 (16/16) 100% |============================================|   3.57 MB  24.12 MB/s Time: 0:00:00
eucalyptus-load-balancer-image-1.0.3-148.img.manifest.xml 100% |===============================================|   5.92 kB  42.48 kB/s Time: 0:00:00
Registered machine image emi-8B64356C
-- Done --
PROPERTY	loadbalancing.loadbalancer_emi	emi-8B64356C was NULL

Load Balancer Support is Enabled

[root@localhost Downloads]# euca-describe-properties loadbalancing.loadbalancer_emi
PROPERTY	loadbalancing.loadbalancer_emi	emi-8ED233C8



euca-modify-property -p loadbalancing.loadbalancer_vm_keyname=admin




[root@localhost Downloads]# euca-modify-image-attribute -l emi-8ED233C8 -a all
launchPermission	emi-8ED233C8	ADD	Group	all


[root@localhost Downloads]# eulb-create-lb -z clearlogy -l "lb-port=80, protocol=HTTP, instance-port=80, instance-protocol=HTTP" ClearElb
DNS_NAME	ClearElb-077577678152.lb.localhost
[root@localhost Downloads]# eulb-describe-lbs
LOAD_BALANCER	ClearElb	ClearElb-077577678152.lb.localhost	2014-01-15T08:53:21.442Z	

[root@localhost Downloads]# eulb-create-lb-listeners -l "lb-port=80, protocol=HTTP, instance-port=80, instance-protocol=HTTP" ClearElb

On Loadbalancer VM,
[root@ip-10-10-1-139 ~]# loadbalancing_loadbalancer_vm_ntp_server=0.centos.pool.ntp.org





