Create windows image from ISO (KVM)

This procedure is all over done on NC where the bridge is configured already.

To stop the NC, enter:

service eucalyptus-nc stop

A template file that closely matches those that Eucalyptus generates at VM instantiation time is located at

/usr/share/eucalyptus/doc/libvirt-kvm-windows-example.xml. 

$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$######################################################################
 WARNING: DON'T USE OTHER TOOLS SUCH AS ovirt, virt-manager FOR CREATING AND VIEWING IMAGE EXCEPT MENTIONED ONES BECAUSE HARDWARE PROFILE #
                                                                                                                                          #
          CHANGES LEADS TO PROBLEM IN BOOTING OF IMAGES i.e. unable to go out of boot.                                                    # 
$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$######################################################################

Now,

Install Base Windows OS

The first task for creating a Windows image is installing a base Windows operating system (OS). To install a base Windows OS using KVM:

1. Log in to the stopped NC server or a host that runs the same hypervisor as the NCs.

2. Go to directory 

   [root@abc]# cd /var/lib/libvirt/images/

3. Create a blank disk file. Specify your Windows VM image name using the parameter of.

   [root@abc images]# dd if=/dev/zero of=windows.2003-Server-32bits.img bs=1M count=1 seek=16999

Important: Your image name must start with the word, windows (all lower-case).

4. [root@abc images]# dd if=/dev/zero of=floppy.img bs=1k count=1474

   [root@abc images]# dd if=/dev/zero of=secondary.img bs=1M count=1 seek=1000

5. Copy the libvirt-kvm-windows-example.xml file to your working directory and rename it to libvirt-kvm-windows.xml.

6.  Open the new libvirt-kvm-windows.xml file and provide fully qualified paths to the VM image file and iso.

    Make sure that the name of the bridge is the same as the one used by the hypervisor on which you are creating the

    Windows image.


Match your code with following code:

####################################################################################################################
# My file is sample for windows 2003 server. llly, You can cerate for Windows 7, 2008 Server, 2012 Server, 8.      #
####################################################################################################################
<domain type='kvm'>
<name>eucalyptus-win-2003</name>
<os>
<type>hvm</type>
<boot dev='cdrom'/>
</os>
<features>
<acpi/>
</features>
<memory>524288</memory>
<vcpu>1</vcpu>
<devices>
<emulator>/usr/libexec/qemu-kvm</emulator>
<disk type='file'>
<source file='/var/lib/libvirt/images/windows_2003.img'/>
<target dev='hda'/>
</disk>
<!-- <disk type='file' device='disk'>
<source file='fully_qualified_path_to_secondary_disk'/>
<target dev='vda' bus='virtio'/>
</disk>
<disk type='file' device='floppy'>
<source file='fully_qualified_path_to_floppy_disk'/>
<target dev='fda'/>
</disk> -->
<disk type='file' device='cdrom'>
<source
file='/var/lib/libvirt/images/windows.2003-Server-32.iso'/>
<target dev='hdc'/>
<readonly/>
</disk>
<interface type='bridge'>
<source bridge='br0'/>
<model type='rtl8139'/>
</interface>
<!--<interface type='bridge'>
<source bridge='br0'/>
<model type='virtio'/>
</interface> -->
<graphics type='vnc' port='-1' autoport='yes' listen='0.0.0.0'/>
</devices>
</domain>
##############################################################################################################
##############################################################################################################

 Check for Domain name, Img file path and ISO file path remaining should be as it is.


7. Start the VM.

[root@abc images]# virsh create libvirt-kvm-windows.xml

8. Connect to the virtual console using the VNC client of your choice.  

   I am using tiger VNC. suppose NC on which your VM is running is 192.168.2.21 then in dialog box type:

      192.168.2.21::5901 

The port numbers from 5900-5910


9. Follow the standard Windows installation procedure until the VM has completed installing Windows.
  
   Tip: On some hosts, the VNC’s display number will change when an image restarts. Use ps to find the current number.

10. Run virsh list to display the domain name.

11. Shut down the Windows VM you have just created. 

    [root@abc images]# virsh destroy eucalyptus-win-2003


Install Eucalyptus Windows Integration


To install the Eucalyptus Windows Integration Service:

1. If you're running a version of Windows more recent than Windows Server 2003, download the most recent version
   of the Windows Image Preparation Tool from http://downloads.eucalyptus.com/software/tools/windows-prep/ to
   /var/lib/libvirt/images on your NC or on the host running the vSphere client.

2. Open the libvirt-kvm-windows-example.xml file you used in the previous section and make the following edits:

•  Change the text so that windows-prep-tools-latest.iso replaces the Windows .iso image and is mounted as cdrom.
•  Enter the path to the secondary disk file you created in the previous task.
•  Uncomment the lines that direct attachment of a floppy disk, secondary disk, and secondary network interface.

Tip: If you plan on using virtio networking for instances (via USE_VIRTIO_NET option on node controllers), 
     uncommenting the virtio interface in the xml is mandatory

####################################################################################################################
#                               Uncomment all except  <boot dev="cdrom">                                           #
####################################################################################################################
<domain type="kvm">
<name>eucalyptus-windows</name>
<os>
<type>hvm</type>
<!-- <boot dev='cdrom'/> -->
</os>
<features>
<acpi/>
</features>
<memory>524288</memory>
<vcpu>1</vcpu>
<devices>
<emulator>/usr/libexec/qemu-kvm</emulator>
<disk type='file'>
<source file='/var/lib/libvirt/images/windows_2003.img'/>
<target dev='hda'/>
</disk>
<disk type='file' device='disk'>
<source file='/var/lib/libvirt/images/secondary.img'/>
<target dev='vda' bus='virtio'/>
</disk>
<disk type='file' device='floppy'>
<source file='/var/lib/libvirt/images/floppy.img'/>
<target dev='fda'/>
</disk>
<disk type='file' device='cdrom'>
<source
file='/var/lib/libvirt/images/windows-prep-tools-legacy.iso'/>
<target dev='hdc'/>
<readonly/>
</disk>
<interface type='bridge'>
<source bridge='br0'/>
<model type='rtl8139'/>
</interface>
<interface type='bridge'>
<source bridge='br0'/>
<model type='virtio'/>
</interface>
<graphics type='vnc' port='-1' autoport='yes' listen='0.0.0.0'/>
</devices>
</domain>
####################################################################################################################
####################################################################################################################

named it as libvirt-kvm-windows-example.xml

3. Start the VM.

virsh create libvirt-kvm-windows-example.xml

4. Log in to Windows and find the Eucalyptus installation files in the CDROM drive.

•  For Windows Server 2003 R2, run setup.exe. This automatically installs the .NET framework 2.0, which is not bundled in Server 2003 R2.

•  For all other versions, run EucalyptusWindowsIntegration.msi. (setup.exe will automatically install .NET framework 2.0, which is not bundled in Server 2003 R2).

6. In the Choose your hypervisor step, select KVM and then click Next.

   Click Next and continue until the end of installation.

7. Reboot the Windows VM

8. Open the Windows device manager and check that the following drivers are found for each device.

•  Floppy disk drive
•  Disk drivers: Red Hat VirtIO SCSI Disk Device
•  SCSI and RAID controllers: Red Hat VirtIO SCSI controller
•  Network adapters: Red Hat VirtIO Ethernet Adapter

If the correct drivers are not found, question marks display on the devices. To install the devices, do the following:
• Right-click on the devices in question and select Update Drivers to open the New Hardware Wizard.
• When the new hardware wizard asks if Windows update is to be connected, click No, not this time.
• Choose Install software automatically (recommended).
• If a confirmation popup message displays, click Continue.


Most of the networks don't have server directory, so I am skipping the active directory part.


Configure Remote Desktop

Domain users or groups require remote desktop permission to log into an instance. 

To configure remote desktop permission:

1. Open the Eucalyptus Windows Integration popup (Windows Programs > Eucalyptus > Eucalyptus Setup).

2. Click the RemoteDesktop tab

The names of authorized domain users and groups display in the Authorized User/Groups field. By default, only
the local administrator is listed as authorized.

3. In the text field below the list, enter a user and group account name in the format [DOMAIN]\[USER or GROUP].

If you add a new local user or local group, prepend the account name like localhost\abc

4. Click Add.

5. Repeat for all user/groups that you want to add.

6. Click Apply.

When the instance launches, the members of the groups you added can log in to the instance through remote desktop.

Run Sysprep

Note: The Eucalyptus Integration Service supports Sysprep for Windows Server 2008, Windows Server 2008 R2 and Windows 7.

To configure and run Sysprep:
1. Open the Eucalyptus Windows Integration popup (Windows Programs > Eucalyptus > Eucalyptus Setup).

2. Click the General tab.

3. Ensure that Format uninitialized drives is checked

4. Click the Run Sysprep button.

Sysprep starts.

6. After Sysprep is complete, close the application and shutdown the Windows VM using the Windows Programs menu.

 
Add Image to Eucalyptus [For instance Store]

Now copy the image to the Walrus machine.

To enable an image as an executable entity, you must bundle and upload the Windows disk image to Walrus, and then register the uploaded image with Eucalyptus.
 
Run the following command to bundle, upload, and register your Windows disk image:

[root@Frontend Euca-Images]# euca-bundle-image -i windows_2003.img -r i386
warning: this image is larger than EC2's size limit
100% |==========================================================================================================================|  16.60 GB  31.10 MB/s Time: 0:09:33
Wrote manifest /var/tmp/bundle-fHy1Xx/windows.win2008server.img.manifest.xml

[root@Frontend Euca-Images]# euca-upload-bundle -b images -m /var/tmp/bundle-fHy1Xx/windows_2003.img.manifest.xml
windows.win2008server.img.part.0   (  1/302) 100% |=============================================================================|  10.00 MB   4.17 MB/s Time: 0:00:02
windows.win2008server.img.part.1   (  2/302) 100% |=============================================================================|  10.00 MB   1.96 MB/s Time: 0:00:05
windows.win2008server.img.part.2   (  3/302) 100% |=============================================================================|  10.00 MB   7.91 MB/s Time: 0:00:01
windows.win2008server.img.part.3   (  4/302) 100% |=============================================================================|  10.00 MB   8.33 MB/s Time: 0:00:01
.
.
.
.
.
.
.
.
windows.win2008server.img.part.301 (302/302) 100% |=============================================================================|   1.67 MB   6.63 MB/s Time: 0:00:00
windows.win2008server.img.manifest.xml 100% |===================================================================================|  48.38 kB 291.78 kB/s Time: 0:00:00
Uploaded images/windows.win2008server.img.manifest.xml

[root@Frontend Euca-Images]# euca-register --name Windows2003Server images/windows_2003.img.manifest.xml
IMAGE	emi-24D83B29

[root@Frontend Euca-Images]# euca-modify-image-attribute -l emi-24D83B29 -a all
launchPermission	emi-24D83B29	ADD	Group	all

Your Windows image is now ready to run as an instance.

For EBS Images:

1. Now launch an instance of this image from user console.

2. Now, create a volume somewhat more size compare to that of img file.

3. Attach the volume to this instance.
 
4. Execute lvdisplay command; 

   Now the last entry will indicate the volume location like this /dev/euca-ebs-storage-vg-vol-CF473F16/euca-vol-CF473F16 which is our LV path.

6. Now execute this command 

   [root@localhost ~]# dd if=windows_2003.img of=/dev/euca-ebs-storage-vg-vol-CF473F16/euca-vol-CF473F16 bs=1M

   /dev/euca-ebs-storage-vg-vol-CF14426E/euca-vol-CF14426E
   8193+0 records in
   8193+0 records out
   8590983168 bytes (8.6 GB) copied, 175.918 s, 48.8 MB/s

7. From user console, detech volume from instance.

8. Now create snapshot from this volume in User console.

8. After completely created, do register as image from snapshot tab,

   and 

   [root@Frontend Euca-Images]# euca-modify-image-attribute -l emi-24D83B29 -a all

   launchPermission	emi-24D83B29	ADD	Group	all

 Your Windows EBS image isn ready now.


 After you register the image, Walrus decrypts the image bundle. This process might take a few minutes for a large

 Windows image to be decrypted. For example, a 10G image requires that you wait about 10 minutes before you launch

 the instance. You can use the euca-describe-bundle-tasks command line utility to check the status of active bundle tasks.

