1. for the error of dependency of this package /usr/lib64/libgdk-x11-2.0.so.0: undefined symbol: _XGetRequest

    run 
    yum install libX11

2. If storage controller is not working & giving null resources follow these steps:

   condition: Storage Controller operation timed out after waiting for 10000 milliseconds for a response from tgtadm command
       cause: tgt daemon on Storage Contrecholler is unresponsive
   initiator: Storage Controller
    location: tgt daemon on Storage Controller
  resolution:
        1) Run 'ps -ef | grep tgtd', look for the process-ID of tgtd.

        2) Kill the tgtd process with 'kill process-ID'.

        3) Start the tgt daemon with 'service tgtd start'.

        4) Run 'tgtadm --op show --mode target', check that it does not hang or return an error.

1. euca-describe-services -E
2. echo $EC2_URL
3. euca-describe-propertiessc
4. sc log
  
3. When creating snapshots from volume, if you will get this error

Failed to create snapshot from volume-xxxx. Try again. 
euca-create-snapshot: error (CreateSnapshotType): java.lang.RuntimeException: Failed to send message CreateStorageSnapshotType to service StorageInternal because: Component that caused exception is: DefaultJavaComponent{StorageInternal.component}. Message payload is of type: CreateStorageSnapshotType

This is the possibly space issue on the Storage Controller machine.

Follow these steps to troubleshoot:

1. Run following commands on SC/Front end

[root@localhost Downloads]# euca-describe-properties | grep volumesize
PROPERTY	clearlogy.storage.maxtotalvolumesizeingb	100
PROPERTY	clearlogy.storage.maxvolumesizeingb	15

Now, go to physical location /var/lib/eucalytpus/volumes and check for space available.
The space must be filled.

2. Now to change this go to admin console-> service components-> walrus -> Walrus object capacity(GB).

Now, it is 100GB.Change it according to space available on the hard disk. I am making it to 125GB. Save it.

3. Now, check for snapshot storage 

[root@localhost Downloads]#  euca-describe-properties | grep snapshotsize
PROPERTY	walrus.storagemaxtotalsnapshotsizeingb	50

[root@localhost Downloads]# euca-modify-property -p walrus.storagemaxtotalsnapshotsizeingb=100
PROPERTY	walrus.storagemaxtotalsnapshotsizeingb	100 was 50

[root@localhost Downloads]#  euca-describe-properties | grep snapshotsize
PROPERTY	walrus.storagemaxtotalsnapshotsizeingb	100

4. Try to create the snapshot. It has to work now.


Notes:
Adjust the euca property for the volume max volume size and the total max volume size as needed.
euca-describe-properties, look for: PROPERTY <parition>.storage.maxvolumesizeingb
Example:
[root@localhost Downloads]# euca-describe-properties | grep volumesize
PROPERTY        Lab-01.storage.maxtotalvolumesizeingb   100
PROPERTY        Lab-01.storage.maxvolumesizeingb        10

Change the setting with the following command. Note that the property name will change from system to system depending upon the zone name. It is best to copy and paste the property name from your system:
      euca-modify-property -p walrus.storagemaxvolumesizeingb=25 (or other size)

NOTE: Keep in consideration the storage.maxtotalvolumesizeingb when increasing storage.maxvolumesizeingb. 
Also be aware of the host OS storage space in /var/lib/eucalyptus/volumes. example: df  -h. Do not over subscribe the Storage Controller's space or user data may be lost.

