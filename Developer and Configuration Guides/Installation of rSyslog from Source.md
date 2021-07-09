# Installing rSyslog from source

### About this Guide
This guide will help you to install rSyslog from its source code on CentOS 7.

### What is rSyslog?
rSyslog is a log management tool focuses on gathering, monitoring and analyzing logs all across the system. 

1. Download rSyslog from [official website of rSyslog]()
  Extract to desired location

2. Install first following packages
I.   libestr(from web)
II.  libee(from web)
III. json-c(from web)
IV.  mysql-server-5.5(from terminal)
V.   libmysqlclient15-dev(from terminal)
VI.  uuid(from terminal)
VII. uuid-dev(from terminal)

3. Now,go into rsylog directory and run

  `./configure --enable-mysql`
  `make`

  It will give error:

  >    /usr/local/include/json/json.h:27:34: fatal error: json_object_iterator.h: No such file or directory compilation terminated.

   Now we have to copy json_object_iterator.h from extracted folder of Json to /usr/local/include/json/. 

   Again issue make command and it will run fine now.

   Issue "make check" to take test of compilation.

   Now run "make install" and then "make installcheck"

   If you do not get any error then congrats rSyslog is installed

   successfully !! 
   


