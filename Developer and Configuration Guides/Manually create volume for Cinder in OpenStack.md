# Manually create volume for Cinder in OpenStack

### About this tutorial
Cinder is volume block service of OpenStack private cloud platform. In this tutorial, we'll see how to assign hard disk space, as a storage, to Cinder.

### Installation

1. To check the free space available on the hard disk, run following command: 
    ```
    df -h
    ```

2. In order to create partition of this free space we'll use GUI tools in Ubuntu like `GParted`, `Disks`.

    In this example, we've used `Disks` for create and format hard disk partition.

3. Go to `Ubuntu Explorer` by pressing `Alt`+`F2` - Disks.
4. Select the free space as per your requirement.
5. Click on `+` icon.
6. Choose Following parameters:
    ```
    Create Partition:
    Erase   : Don't overwrite existing data(quick)
    Type    : Compatible with all linux systems (ext4)
    Name    : cinder-volumes
    ```
    Now, you will have `cinder-volumes` named partition which is unmounted.

    Note that this line: `Device /dev/sda3` might be different as per configurations and devices.

7. To mount the partition, go to Terminal as root user.
8. Run this command:
    ```
    pvcreate /dev/sda3 \
    vgcreate cinder-volumes /dev/sda3
    ```

You have successfully created the volume for Cinder.
