# Installation of DevStack on Ubuntu

## About this guide
DevStack is an single box installation of necessary services of OpenStack in order to test and develop OpenStack services and applications.

**Note:** These instructions are applicable to both single machine and virtual machine.

## Prerequisites
- *Operating Systems:* Ubuntu 20.04 LTS
- *Architecture:* x64 bits
- *Hard Disk Drive:* 30 GB Minimum Recommended
- *RAM:* 2 GB


## Steps for Installation:

1. Login to Ubuntu.
   
2. Execute the following commands.
   
   To update update all Ubuntu packages:
   ```
   sudo apt-get -qqy update
   ```
   To install `git` for fetching latest code from GitHub
   ```
   sudo apt-get install -qqy git
   ```
   Clone the repository:
   ```
   git clone https://github.com/openstack-dev/devstack.git
   ```
   ```
   cd devstack
   ```
3. Execute following commands:
   ```
   echo '[[local|localrc]]' > local.conf
   ```
   ```
   echo ADMIN_PASSWORD=password >> local.conf
   ```
   ```
   echo MYSQL_PASSWORD=password >> local.conf
   ```
   ```
   echo RABBIT_PASSWORD=password >> local.conf
   ```
   ```
   echo SERVICE_PASSWORD=password >> local.conf
   ```
   ```
   echo SERVICE_TOKEN=tokentoken >> local.conf
   ```
4. After copying required credentials into local.conf file, run the shell script:
   ```
   ./stack.sh
   ```
5. Now your DevStack  environment is ready to use.
   
---
**Additional Note:**

- You can perform following tasks for optimizations:

  - *Stop checking for periodic downloading of updates from GitHub:*

      - Edit `devstack/localrc`
      - Set value as shown: `RECLONE=no`
      - Interface of VM/System, where you see IP address (new IP address)
        Set value as shown: `PUBLIC_INTERFACE=eth0`
      - Save the file & reboot.


  - *OpenStack services not starting after reboot*
  
      Problem with reboot is, except Dashboard, rest of the OpenStack services won't start. To start all services, run following commands:
      ```
      # ./unstack.sh
      ```
      ```
      # ./stack.sh
      ```
      Let the process to complete & you will see IP address at the finish. 
      
      This is OpenStack Horizon Dashboard IP address which you can also access from web browser.