To launch a Windows machine, follow these instructions.

Launch Windows Instance

1. Go to Images 

2. Click to launch instances

3. Select resources to launch instances as shown in figure

4. Select keypair and security group

5. You will see the instance notification in the user console.

To ensure an instance, wait for Instance status in the User console.

Once an instance is shown in Running state, use one of the following procedures:

Select the running windows machine which you want to connect

Click on “Connect“ to get password of Administrator account of windows
[By default, user: pmcuser and password: pmc1234 is accessible on all windows machines.]

6. Click on “get password for admin”

7. Choose admin.pem file

8.  You will see the password required to connect with Windows Machine

9. Now you can use the Remote Desktop to connect with this machine.


To Attach Extra Storage

10. Go to Storage -> Volumes

11. To create new volume of desired size, see below

12. After clicking on Create Volume it will create new volume as follows

13. Wait for available state of volume, after completion attach it to running instance

14.  Enter Name of instance as follows

15. After attach, in console it will go in the in-use state which means volume is available in windows.

Go to My Computer -> Manage -> Device Management, and right click on disk 1 and select

“Initialize Disk” as shown below:

16.  Now disk 1 online. So format it in regular manner as shown below:

17. Now your volume is ready for the storage of data.

18.  You will see same in explorer and your additional storage is ready.
