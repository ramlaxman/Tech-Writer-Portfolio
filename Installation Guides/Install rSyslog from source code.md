# Install rSyslog from source code

## About this Guide
This guide will help you to install rSyslog from its source code on CentOS 7.

## What is rSyslog?
`rSyslog` is a log management server focuses on gathering, monitoring and analyzing logs. It gathers various file formats all across the system, transforms them and send the output to different file formats like HDFS (Hadoop), hiredis (Redis). It has capacity of processing of one million messages/second to local destinations.

## Steps to install rSyslog:
1. Download rSyslog from [official website of rSyslog](https://www.rsyslog.com/files/download/rsyslog/rsyslog-8.2106.0.tar.gz) and extract to desired location.

2. Install the following packages:
  
    *Hint:* You can use [CentOS packages website](https://centos.pkgs.org/7/centos-x86_64/) for the same.

   1. libestr
   2. libee 
   3. json-c
   4. mysql-server-5.5
   5. libmysqlclient15-dev
   6. uuid
   7. uuid-dev


3. Now, go into rSyslog directory and run:

    ```
    ./configure --enable-mysql
    ```
    ```
    make
    ```
4. Run the following command to install and check for issues, if there are any: 
   ```
   make check
   ``` 
   ```
   make install
   ``` 
   ```
   make installcheck
   ```
  This concludes successful installation of rSyslog.

<br>

---
***Note:*** If you are getting error after step 3:

  > /usr/local/include/json/json.h:27:34: 
  >
  > fatal error: json_object_iterator.h:
  >
  > No such file or directory compilation terminated.


Refer to the following steps.

- Copy `json_object_iterator.h` from extracted folder of json to `/usr/local/include/json/`

- Run `make` command again and it should run fine.
