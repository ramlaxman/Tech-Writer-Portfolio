SSH on Linux

To remove previous SSH credentials,

ssh-keygen -R 192.168.100.1


Command for SFTP for copying remote machine file to local machine

[root@ip-10-10-1-77 ~]# scp -p root@192.168.2.20:/root/Downloads/bitnami-lampstack-5.4.23-0-linux-x64-installer.run /root/Downloads/
The authenticity of host '192.168.2.20 (192.168.2.20)' can't be established.
RSA key fingerprint is 91:b2:0a:0a:a6:75:1f:e1:5a:be:46:1d:3e:b9:17:bd.
Are you sure you want to continue connecting (yes/no)? Yes
Warning: Permanently added '192.168.2.20' (RSA) to the list of known hosts.
root@192.168.2.20's password: 

bitnami-lampstack-5.4.23-0-linux-x64-installer.run   100%   68MB  6.8MB/s  00:10 
To make Windows Time synchronize with NTP server

Stop the W32Time service with : C:\>net stop w32time
Configure the external NTP server by  typing : C:\> w32tm /config /syncfromflags:manual /manualpeerlist: 0.centos.pool.ntp.org
Then make your  PDC a reliable NTP server with  C:\>w32tm /config /reliable:yes
Start the w32time service with : C:\>net start w32time
You can check the NTP servers configuration by typing: C:\>w32tm /query /configuration
Next thing I decided to do was to automate the time sync, since I didn’t want to rely on Windows to do it.
Command for that is pretty simple : c:\w32tm /resync

Installation
By default the tree command is not installed. Type the following command to install the same under RHEL / CentOS / Fedora Linux:

# yum install tree

If you are using Debian / Mint / Ubuntu Linux, type the following command to install the tree command:
$ sudo apt-get install tree
