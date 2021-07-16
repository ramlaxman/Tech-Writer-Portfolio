1 Preliminary Note

I'm using a CentOS 6.3 server with the hostname server1.example.com and the IP address 192.168.0.100 here as my KVM host.

I had SELinux disabled on my CentOS 6.3 system. I didn't test with SELinux on; it might work, but if not, you better switch off SELinux as well:

vi /etc/selinux/config

Set SELINUX=disabled...

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of these two values:
#     targeted - Targeted processes are protected,
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted

... and reboot:

reboot

We also need a desktop system where we install virt-manager so that we can connect to the graphical console of the virtual machines that we install. I'm using a Fedora 17 desktop here.

 
2 Installing KVM

CentOS 6.3 KVM Host:

First check if your CPU supports hardware virtualization - if this is the case, the command

egrep '(vmx|svm)' --color=always /proc/cpuinfo

should display something, e.g. like this:

[root@server1 ~]# egrep '(vmx|svm)' --color=always /proc/cpuinfo
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall
 nx mmxext fxsr_opt rdtscp lm 3dnowext 3dnow pni cx16 lahf_lm cmp_legacy svm extapic cr8_legacy misalignsse
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall
 nx mmxext fxsr_opt rdtscp lm 3dnowext 3dnow pni cx16 lahf_lm cmp_legacy svm extapic cr8_legacy misalignsse
[root@server1 ~]#

If nothing is displayed, then your processor doesn't support hardware virtualization, and you must stop here.

Now we import the GPG keys for software packages:

rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY*

To install KVM and virtinst (a tool to create virtual machines), we run

yum install kvm libvirt python-virtinst qemu-kvm

Then start the libvirt daemon:

/etc/init.d/libvirtd start

To check if KVM has successfully been installed, run

virsh -c qemu:///system list

It should display something like this:

[root@server1 ~]# virsh -c qemu:///system list
 Id Name                 State
----------------------------------

[root@server1 ~]#

If it displays an error instead, then something went wrong.

Next we need to set up a network bridge on our server so that our virtual machines can be accessed from other hosts as if they were physical systems in the network.

To do this, we install the package bridge-utils...

yum install bridge-utils

... and configure a bridge. Create the file /etc/sysconfig/network-scripts/ifcfg-br0 (please use the IPADDR, PREFIX, GATEWAY, DNS1 and DNS2 values from the /etc/sysconfig/network-scripts/ifcfg-eth0 file); make sure you use TYPE=Bridge, not TYPE=Ethernet:

vi /etc/sysconfig/network-scripts/ifcfg-br0

DEVICE="br0"
NM_CONTROLLED="yes"
ONBOOT=yes
TYPE=Bridge
BOOTPROTO=none
IPADDR=192.168.0.100
PREFIX=24
GATEWAY=192.168.0.1
DNS1=8.8.8.8
DNS2=8.8.4.4
DEFROUTE=yes
IPV4_FAILURE_FATAL=yes
IPV6INIT=no
NAME="System br0"

Modify /etc/sysconfig/network-scripts/ifcfg-eth0 as follows (comment out BOOTPROTO, IPADDR, PREFIX, GATEWAY, DNS1, and DNS2 and add BRIDGE=br0):

vi /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE="eth0"
#BOOTPROTO=none
NM_CONTROLLED="yes"
ONBOOT=yes
TYPE="Ethernet"
UUID="73cb0b12-1f42-49b0-ad69-731e888276ff"
HWADDR=00:1E:90:F3:F0:02
#IPADDR=192.168.0.100
#PREFIX=24
#GATEWAY=192.168.0.1
#DNS1=8.8.8.8
#DNS2=8.8.4.4
DEFROUTE=yes
IPV4_FAILURE_FATAL=yes
IPV6INIT=no
NAME="System eth0"
BRIDGE=br0

Restart the network...

/etc/init.d/network restart

... and run

ifconfig

It should now show the network bridge (br0):

[root@server1 ~]# ifconfig
br0       Link encap:Ethernet  HWaddr 00:1E:90:F3:F0:02
          inet addr:192.168.0.100  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::21e:90ff:fef3:f002/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:8 errors:0 dropped:0 overruns:0 frame:0
          TX packets:27 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:460 (460.0 b)  TX bytes:2298 (2.2 KiB)

eth0      Link encap:Ethernet  HWaddr 00:1E:90:F3:F0:02
          inet6 addr: fe80::21e:90ff:fef3:f002/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:18455 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11861 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:26163057 (24.9 MiB)  TX bytes:1100370 (1.0 MiB)
          Interrupt:25 Base address:0xe000

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:5 errors:0 dropped:0 overruns:0 frame:0
          TX packets:5 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:2456 (2.3 KiB)  TX bytes:2456 (2.3 KiB)

virbr0    Link encap:Ethernet  HWaddr 52:54:00:AC:AC:8F
          inet addr:192.168.122.1  Bcast:192.168.122.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)

[root@server1 ~]#

