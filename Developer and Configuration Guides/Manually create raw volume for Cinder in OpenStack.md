# Manually create raw volume for Cinder in OpenStack

### About this tutorial
Cinder is volume block service of OpenStack private cloud platform. In this tutorial, we'll see how to assign hard disk space, as a storage, to create volume in Cinder.

### Installation

We need to some free space available for Cinder volume service. Now I have 145 GB free space, to make it accessible I have done following things:

Create free space by using tools in Ubuntu like `GParted`, `Disks`. To do so, follow the steps:

1. Go to Ubuntu Explorer by pressing `Alt`+`F2` - Disks.
2. Select the free space as per your requirement.
3. Click on `+` icon.
4. Choose Following parameters:
    ```
    Create Partition:
    Erase   : Don't overwrite existing data(quick)
    Type    : Compatible with all linux systems (ext4)
    Name    : cinder-volumes
    ```
    Now, you will have `cinder-volumes` named partition which is unmounted.

    Note that this line: `Device /dev/sda3` might be different as per configurations and devices.

5. To mount the partition, go to Terminal as root user.
6. Run this command:
    ```
    pvcreate /dev/sda3 \
    vgcreate cinder-volumes /dev/sda3
    ```

You have successfully created the raw volume for Cinder.

