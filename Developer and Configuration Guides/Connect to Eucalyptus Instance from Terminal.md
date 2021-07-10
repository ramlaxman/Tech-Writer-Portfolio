# Connect to Eucalyptus Instance from Terminal

1.  `[root@localhost Downloads]#`
	```
	ssh -i admin.pem root@192.168.2.103
	```
    **Output:**
    > The authenticity of host '192.168.2.103 (192.168.2.103)' can't be established. 
	>
	> RSA key fingerprint is 52:36:5b:1a:dd:62:fb:56:a7:92:99:5a:92:e1:29:27.
	> 
	> Are you sure you want to continue connecting (yes/no)? yes
	> 
	> Warning: Permanently added '192.168.2.103' (RSA) to the list of known hosts.

2.	`[root@ip-10-10-1-113 ~]#`
	```
	yum install httpd nc wget ntp
	```

3.  `[root@ip-10-10-1-113 ~]#` 
	```
	vi /var/www/html/index.html
	```
	Edit file with ```Hello World!``` and save.

4.  `[root@ip-10-10-1-113 ~]#` 
   	```
   	service httpd start
   	```
   	**Output:**
   	> Redirecting to /bin/systemctl start  httpd.service

5.  `[root@ip-10-10-1-113 ~]#` 
   	```
   	wget http://192.168.2.103/index.html
   	```
   	**Output:**
   	> --2014-02-03 08:43:13--  http://192.168.2.103/index.html
   	>
   	> Connecting to 192.168.2.103:80... connected.
   	>
   	> HTTP request sent, awaiting response... 200 OK
   	>
   	> Length: 23 [text/html]
   	>
   	> Saving to: `index.html'
   	>
   	> 100%[=============================================================================================================================>] 
   	> 23          --.-K/s   in 0s
   	>
	> 2014-02-03 08:43:13 (3.50 MB/s) - `index.html' saved [23/23]

6.  `[root@ip-10-10-1-113 ~]#` 
   	```
   	ntpdate -u 0.centos.pool.ntp.org
   	```
   	**Output:**
   	> 3 Feb 03:13:32 ntpdate[838]: step time server 120.88.46.10 offset -19801.820211 sec
7.  `[root@ip-10-10-1-113 ~]#` 
   	```
   	nc -z 192.168.2.100 80
   	```
	**Output:**
   	> Connection to 192.168.2.100 80 port [tcp/http] succeeded!

8.  `[root@ip-10-10-1-113 ~]#` 
   	```
   	nc -z 192.168.2.103 80
   	```
   	**Output:**
   	> Connection to 192.168.2.103 80 port [tcp/http] succeeded!
   
9.	`[root@ip-10-10-1-113 ~]#` 
	```
	vi /etc/ntp.conf 
	```
    Edit file and append `0.centos.pool.ntp.org` at the end of file.

10.	`[root@ip-10-10-1-113 ~]#` 
	```
	service ntpd restart
	```
	**Output:**
	> Redirecting to /bin/systemctl restart  ntpd.service

11.	`[root@ip-10-10-1-113 ~]#` 
	```
	service ntpd stop
	```
	**Output:**
	> Redirecting to /bin/systemctl stop  ntpd.service

12.	`[root@ip-10-10-1-113 ~]#` 
	```
	service ntpd start	
	```
	**Output:**
	> Redirecting to /bin/systemctl start  ntpd.service
13.	`[root@ip-10-10-1-113 ~]#` 
	```
	vi index.html 
	```
	
14.	`[root@ip-10-10-1-113 ~]#` 
	``` 
	ntpdate -u 0.centos.pool.ntp.org 
	```
	**Output:**
	>  3 Feb 03:21:41 ntpdate[879]: adjust time server 123.108.225.6 offset 0.006551 sec

15.	`[root@ip-10-10-1-113 ~]#` 
	``` 
	ntpq -p 
	```
   	**Output:**
	```
	remote           refid      st t when poll reach   delay   offset  jitter
	==============================================================================
	*ns02.hns.net.in 200.98.196.212   2 u   26   64    1   14.894    7.962   1.407
	 web10.hnshostin 10.84.87.146     2 u   27   64    1   26.089   -1.469   1.000
	 120-88-47-10.in 103.1.106.69     2 u   26   64    1   19.906    6.017   1.272
	```

