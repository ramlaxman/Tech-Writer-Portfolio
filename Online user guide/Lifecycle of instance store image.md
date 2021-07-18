Eucalyptus
Lifecycle of an Instance store backed Image
Eucalyptus Versions: 3.4.2 with KVM hypervisor only
Overview
This article covers the lifecycle of an instance store backed image all the way through its first upload to Walrus until it is used to create an instance on the Eucalyptus cloud and in the end how it can be deregistered and removed from Walrus.
This would serve the purpose of helping Cloud administrators  debug problems with images on their cloud because the finer level details it touches gives an overview of how stuff works!

Upload to Walrus
There are various ways to upload your favourite image to the cloud. In this article we focus only on the Instance store backed images that are uploaded on walrus. The way people usually do it using either eustore or the euca-bundle-image->euca-upload-bundle->euca-register.
For the purpose of this article we would use the eustore method of uploading and registering and image as that is simple and job done in 1 command. The command we issue after source'ing our credentials is
eustore-install-image -i 0355237665 -b fedora20
The command finishes with a message saying
Installed new image emi-D5EF3577
In the backend, once it gets uploaded to walrus it is stored on the filesystem mounted at /var/lib/eucalyptus/bukkits/ , inside a directory that has the same name as the bucket name (fedora20 in this case).
We can navigate to the directory and see the various files in there. As soon as the image gets registered the Walrus gets the image in its cache. Please note unless this is done the image will not be available to the node controllers when they would like to run an instance from it.
If you cloud is logging at debug level (controlled by cloud property cloud.euca_log_level) you can see a message like following in your Walrus cloud-output.log
2014-02-16 12:13:16  INFO 000079838 Images                   | Triggering cache population in Walrus for: emi-D5EF3577
This indicates walrus has triggered the caching of the image.
The caching takes some time depending on the size of images. Normally the Linux images are smaller in sizes hence caching happens pretty quickly. But for large windows images of sizes more than 10GB etc. it could take some more time usually it depends on various things like the hardware resources available to the Walrus etc.
We have put the detailed level logs for the caching at Walrus here 
As can be seen the Walrus does the cache population for the kernel, ramdisk and root filesystem. It took almost 2 minutes in this case (2GB size of root filesystem).
We can grep for "WalrusImageManager" and "Images" in the log file to find out the relevant portion about the image caching at Walrus end.

Transfer to Node Controller
Once the image is cached on the Walrus we can start using it by creating an instance from this image. The instance run request goes to a node controller selected by the scheduling policy established in the cluster controller.
Once the node controller receives the request to run the instance from a given emi it then request walrus to give the required files to it. Following can be seen on the node controller when the instance run request comes.

Logs
As seen in the log snippet above, the NC downloads the image from Walrus cache and copies it to the local cache at the NC usually located at /var/lib/eucalyptus/instances/cache/ with a directory for the EMI used (in this case emi-D5EF3577-c7358e8c/).
Once the NC has finished caching the image it will then prepare the instance artifacts and use the image in cache to boot the instance. All this is done inside /var/lib/eucalyptus/instances/work/
also visible in the logs.
If for some reason the walrus is in the process of caching the image at its end and the NC queries for the image, it will fail.
The NC will continue to query and we can configure the number of retries in eucalyptus.conf of NC by modifying the variable WALRUS_DOWNLOAD_MAX_ATTEMPTS (Min 1, default 9, max 98). This could be handy when dealing with large images.
Instance having problem
If the instance did not come up properly due to some problem , perhaps networking etc. we can identify the problem by checking the console output using euca-get-console-output command. If we like to try few things when the instance comes up to debug the problem further we can modify the image stored at the Node controller cache (in this case /var/lib/eucalyptus/instances/cache/emi-D5EF3577-c7358e8c/) and then run a new instance from the same image on the same NC.
If we run a new instance from the same image on the same NC the NC will use its local copy of the image instead of downloading it from Walrus.
The blocks file in the EMI directory on the local cache at NC contains the root filesystem. It can be loop mounted on the NC and configuration changes can be done there like this:
mkdir /tmp/1
mount -o loop /var/lib/eucalyptus/instances/cache/emi-D5EF3577-c7358e8c /tmp/1
Now we can either navigate into /tmp/1 or create a chroot environment in /tmp/1 , do our modifications and once done unmount the blocks file.
cd ~
umount /tmp/1
Now if we run the instance again from the same image on the same NC it will pick up the changes we have done to the image. This helps in debugging issues with the image without performing the upload to walrus again and going through the beginning of the lifecycle.
De-registration and Deletion
Once we do not want the image anymore on our cloud we can easily de-register it and delete it from the Walrus. Easy way to do it is to first confirm there are no running instances on the cloud using the same image. If so we need to terminate all these instances.
The images in our case has the following details
IMAGE emi-D5EF3577 fedora20/euca-fedora20-fedora-2013.12.18-x86_64.img.manifest.xml 520745772130 available private x86_64 machine eki-FE363899 eri-8EFE360A instance-store paravirtualized
IMAGE eki-FE363899 fedora20/vmlinuz-3.11.10-301.fc20.x86_64.manifest.xml 520745772130 available private x86_64 kernel instance-store
IMAGE eri-8EFE360A fedora20/initramfs-3.11.10-301.fc20.x86_64.img.manifest.xml 520745772130 available private x86_64 ramdisk instance-store
Note the bucket name is "fedora20" and the prefix for rootfs is "euca-fedora20-fedora-2013.12.18-x86_64.img" (everything before ".manifest.xml"), for ramdisk is "initramfs-3.11.10-301.fc20.x86_64.img" and for the kernel it is "vmlinuz-3.11.10-301.fc20.x86_64"
After terminating the instances we can then de-register the image like this:
euca-deregister emi-D5EF3577
euca-deregister eki-FE363899
euca-deregister eri-8EFE360A
After the de-registration is done we can easily delete the bucket as well as the files within it by executing the following command
euca-delete-bundle -p euca-fedora20-fedora-2013.12.18-x86_64.img -b fedora20 --clear
euca-delete-bundle -p initramfs-3.11.10-301.fc20.x86_64.img -b fedora20 --clear
euca-delete-bundle -p vmlinuz-3.11.10-301.fc20.x86_64 -b fedora20 --clear
The first 2 command will give an error saying 
euca-delete-bundle: error (BucketNotEmpty): The bucket you tried to delete is not empty.
This can be simply ignored as all ramdisk, kernel and root filesystem existed in the same bucket. So unless all is clear bucket cannot be deleted. 
The last delete-bundle will delete all the files and the bucket ultimately.

[URL](https://docs.google.com/document/d/1l7f8vBoCQLbaaAMK8tXMlCSw1urX_hJag5DOxplD4xI/edit#)