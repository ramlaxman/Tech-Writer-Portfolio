Boot the system from the CD using CentOS-6.3-x86_64-bin-DVD1.iso
After some screen, the installation will ask for the user name and password for the system. This is the password for the root.
Whenever promoted for the disk layout, choose the last option customize now and create the following partitions as follows:
/boot -> 2000 MB
/swap -> double of the ram size
/ -> remaining space in the disk
Install the desktop version of the installation
After selecting the Desktop click on the customize now button and choose the packages that you need (some of the minimum are provided here):
Base
Client Management Tools
Net Tools
Development
Server
Additional
Development
Desktop
Servers
System Administration Tools
Virtual
All options
Desktop
KDE Desktop
The installation will install all the packages that have been selected.
After the installation gets completed, provide the user details and boot the system.
Now the centos system is ready to use.
After the completion of installing the OS, the first step is to do the update. The command for this is
yum update
install ntp
After the update is finished, disabled the SELinux. The command is as follows:
vi /etc/selinux/config -> after the file is open changed the value of SELINUX=disabled and restart the machine
Open the file vi /etc/ntp and add the following two lines in the file
server ipaddress iburst
restrict ipaddress mask netmask nomodify notrap
run the command chkconfig ntpd on
run the command service ntpd start
run the command ntpdate -u <your_ntp_server>
run the command hwclock --systohc
iptables --flush
Now the system is ready to install eucalyptus
Run the commands provided in the installation guide of Eucalyptus and start running the following commands:
yum install bridge-utils
Open the network script for the device you are adding to the bridge and add your bridge device to it. The edited file should look similar to the following:
DEVICE=eth0
# change the hardware address to match the hardware address your NIC uses
HWADDR=00:16:76:D6:C9:45
ONBOOT=yes
BRIDGE=br0
NM_CONTROLLED=no
Create a new network script in the /etc/sysconfig/network-scripts directory called ifcfg-br0 or something similar. The br0 is the name of the bridge, but this can be anything as long as the name of the file is the same as the DEVICE parameter, and the name is specified correctly in the previously created physical interface configuration (ifcfg-ethX).
If you are using DHCP, the configuration will look similar to:
DEVICE=br0
TYPE=Bridge
BOOTPROTO=dhcp
ONBOOT=yes
DELAY=0
If you are using a static IP address, the configuration will look similar to:
DEVICE=br0
TYPE=Bridge
BOOTPROTO=static
IPADDR=<static_IP_address>
NETMASK=<netmask>
GATEWAY=<gateway>
ONBOOT=yes
Enter the following command:
service network restart


Run the following commands to install the Eucalyptus commands:
yum install http://downloads.eucalyptus.com/software/eucalyptus/3.2/centos/6/x86_64/eucalyptus-release-3.2.noarch.rpm
 
yum install http://downloads.eucalyptus.com/software/euca2ools/2.1/centos/6/x86_64/euca2ools-release-2.1.noarch.rpm
 
yum install http://downloads.eucalyptus.com/software/euca2ools/2.1/centos/6/x86_64/euca2ools-release-2.1.noarch.rpm
 
yum install http://downloads.eucalyptus.com/software/eucalyptus/3.2/centos/6/x86_64/elrepo-release-6.noarch.rpm
 
yum install eucalyptus-nc
 
ls -l /dev/kvm
 
Verify the op of the above command
 
crw-rw-rw- 1 root kvm 10, 232 Nov 30 10:27 /dev/kvm
 
yum groupinstall eucalyptus-cloud-controller
 
yum install eucalyptus-cc eucalyptus-sc eucalyptus-walrus
Configure the Eucalyptus components:
Open the  file vi /etc/eucalyptus/eucalyptus.conf and change the following lines
Under the Cluster Controller Configuration change the following values
NODES= “ipaddress of node1, ipaddress of node2...etc”
Under the Networking Configuration
VNET_MODE=”suitable mode” (in college MANAGED-NOVLAN)
VNET_PRIVINTERFACE=”eth0”
VNET_PUBINTERFACE=”eth0”
VNET_BRIDGE=”name to bridge” (for eg br0)
VNET_PUBLICIPS=”public ip address these ip’s should be of the same range that is provided to the systems in the Eucalyptus”
VNET_NETMASK=”netmask of the system”
VNET_DNS=”if dns server is available then add”
VNET_DHCPUSER=”dhcpd41”
Start the Eucalyptus services
Start the Cloud Controller
/usr/sbin/euca_conf –initialize
Start the Walrus
service eucalyptus-cloud start
Start the CC
service eucalyptus-cloud start
Start the SC
service eucalyptus-cloud start
Start all the NC’s
service eucalyptus-nc start
Register the Eucalyptus Components

Register the Secondary Cloud Controller

/usr/sbin/euca_conf --register-cloud --partition eucalyptus 
--host [Secondary_CLC_IP] --component [CLC_Name]

Recommended: [CLC_NAME] = CLC-[hostname of the clc machine]

Register the Walrus

/usr/sbin/euca_conf --register-walrus --partition walrus --host [walrus_IP_address] --component [walrus_name]

Recommended: [walrus_name]= walrus-[hostname of the walrus machine]

Register the CC

/usr/sbin/euca_conf --register-cluster --partition [partition_name]
 --host [CC_IP_address] --component [cc_name]

Recommended: [partition_name]= cluster01
		    [cc_name]= cc-[hostname or ipadd of cc machine]

Register the SC

/usr/sbin/euca_conf --register-sc --partition [partition_name] --host [SC_IP_address]	--component [SC_name]

Recommended: [partition_name]=[partition name of cc]
		    [SC_name] = sc-[hostname]


Register the NC

/usr/sbin/euca_conf --register-nodes "[node0_IP_address] ... [nodeN_IP_address]"

Configuring the runtime environment
To generate a set of credentials run the following commands
		/usr/sbin/euca_conf --get-credentials admin.zip
		unzip admin.zip
Source the file by running the following commands
		source eucarc
Configure the storage controller
Configure the SC to use the OverlayManager for storage.
	euca-modify-property -p <partition>.storage.blockstoragemanager=overlay
The output of the command should be similar to:
	PROPERTY	PARTI00.storage.blockstoragemanager	overlay was <unset>
Verify that the property value is now: 'overlay'
	euca-describe-properties | grep blockstorage


Now the system is ready to run the EUCALYPTUS Cloud
Verify the availability zones by running the following commands:
euca-describe-availability-zones verbose
The resources should be listed in the list that are available for the use

References:
Download the ISO from the following link
https://archive.org/download/centos-6.3_release/CentOS-6.3-x86_64-bin-DVD1.iso


Link for the Installation Guide
http://www.eucalyptus.com/docs/eucalyptus/3.2/ig/
