Image<- Snapshot <- Volume <- Windows Image 

Steps are as follows:
1. Launch a instance from windows based instacne store.

   For windows based instance store image procedure as follows:

   [root@Cloud images]# euca-bundle-image -i windows.windowsultimate.img -r x86_64

   Wrote manifest /var/tmp/bundle-Mmluia/windows.windowsultimate.img.manifest.xml

   [root@Cloud images]# euca-upload-bundle -b images -m /var/tmp/bundle-Mmluia/windows.windowsultimate.img.manifest.xml

   windows.windowsultimate.img.manifest.xml 100% |===========================|  41.81 kB 281.97 kB/s Time: 0:00:00
   Uploaded images/windows.windowsultimate.img.manifest.xml

   [root@Cloud images]# euca-register --name windowsulimate images/windows.windowsultimate.img.manifest.xml
   IMAGE    emi-DE6E3E39

   You can see the image using euca2ools euca-describe-images.

   To make image attribute public

   [root@localhost Downloads]# euca-modify-image-attribute -l -a all emi-8ED233C8
    launchPermission	emi-8ED233C8	ADD	Group	all

   To reverse this i.e. to make it available only to Private accounts

   [root@localhost Downloads]# euca-modify-image-attribute -l -r all emi-8ED233C8
    launchPermission	emi-8ED233C8	REMOVE	Group	all

 

2. Now launch an instance of this image from user console.

3. Now, create a volume somewhat more size compare to that of img file.

4. Attach the volume to this instance.
 
5. Execute lvdisplay command; now the last entry will indicate the volume location like this /dev/euca-ebs-storage-vg-vol-CF473F16/euca-vol-CF473F16 which is 
 our LV path.

6. Now execute this command 

   [root@localhost ~]# dd if=windows.windowsultimate.img of=/dev/euca-ebs-storage-vg-vol-CF473F16/euca-vol-CF473F16 bs=1M

/dev/euca-ebs-storage-vg-vol-CF14426E/euca-vol-CF14426E

   8193+0 records in
   8193+0 records out
   8590983168 bytes (8.6 GB) copied, 175.918 s, 48.8 MB/s

7. Now run euca-describe-snapshots which will give you the snapshot creating status.

8. After created run euca-register --name <image-name> --snapshot <snapshot-id> --root-device-name <device>

