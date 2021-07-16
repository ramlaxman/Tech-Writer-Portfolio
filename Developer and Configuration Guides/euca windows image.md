[root@Cloud images]# euca-bundle-image -i windows.win2008server.img -r x86_64
warning: this image is larger than EC2's size limit
100% |==========================================================================================================================|  16.60 GB  31.10 MB/s Time: 0:09:33
Wrote manifest /var/tmp/bundle-fHy1Xx/windows.win2008server.img.manifest.xml


[root@Cloud images]# euca-upload-bundle -b images -m /var/tmp/bundle-fHy1Xx/windows.win2008server.img.manifest.xml
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

[root@Cloud images]# euca-register --name Windows2008Server images/windows.win2008server.img.manifest.xml
IMAGE	emi-24D83B29
[root@Cloud images]# euca-modify-image-attribute -l emi-24D83B29 -a all
launchPermission	emi-24D83B29	ADD	Group	all



