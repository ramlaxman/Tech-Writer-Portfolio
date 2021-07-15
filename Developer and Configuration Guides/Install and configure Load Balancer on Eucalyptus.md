# Install and configure Load Balancer on Eucalyptus

### Prerequisites:
- Minimum 2 running instances
- EucaLobo

### Steps:
To create Load Balancer from EucaLobo:

1. Go to `EC2 Networking` - `Load Balancers` - `Create`.

2. Choose the following configurations:
   - Name: Exam
   - Protocol: TCP
     Check availability zones.
   - Ping protocol: TCP
   - Healthy threshold: 3

     Rest are same.

**Recommended approach:** *Do not register instances with Load Balancing VM.*

### Configuration on Loadbalancer

1. `[root@localhost Downloads]#` 
   ```
   ssh -i admin.pem root@192.168.2.100
   ```
2. `[root@ip-10-10-1-113 ~]#`
   ```
   yum install wget httpd nc
   ```
3. `[root@ip-10-10-1-113 ~]#` 
   ```
   service httpd start
   ```
   You'll see the following output:
   
   > Starting httpd: httpd: Could not reliably determine the server's fully qualified domain name, using 10.10.1.113 for ServerName   [ OK ]
   
4. `[root@ip-10-10-1-113 ~]#` 
   ```
   vi /var/www/html/index.html
   ```
5. `[root@ip-10-10-1-113 ~]#` 
   ```
   restorecon -vR /var/www/html/
   ```
6. `[root@ip-10-10-1-113 ~]#` 
   ``` 
   getenforce
   ```
   Output:
   > Disabled

7. `[root@ip-10-10-1-113 ~]#` 
   ```
   iptables -nvL
   ```
   You'll see the following outputs:
   
   > Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
   pkts bytes target     prot opt in     out     source               destination        
   >
   > Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
   pkts bytes target     prot opt in     out     source               destination        
   >
   >Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
   pkts bytes target     prot opt in     out     source               destination        
   
8. `[root@ip-10-10-1-113 ~]#` 
   ```
   iptables -F
   ```
9. `[root@ip-10-10-1-113 ~]#` 
   ```
   service iptables save
   ```
   You'll see the following outputs:
   > iptables: Saving firewall rules to /etc/sysconfig/iptables: [ OK ]
   
 
10. `[root@ip-10-10-1-113 ~]#` 
    ```
    ntpq -p
    ```
    You'll see following output:
    ```
    remote  refid  st t when poll reach   delay   offset  jitter
    =======================================================================
    dnspun.net4indi 140.109.1.10     3 u   18   64    7   16.053   43.789  11.630
    ```
 
11. `[root@ip-10-10-1-113 ~]#` 
    ```
    vi /etc/ntp.conf
    ```
    Add `0.centos.pool.ntp.org` line at the end of `ntp.conf` file.
 
12. `[root@ip-10-10-1-113 ~]#` 
    ```
    service ntpd restart
    ```
    You'll see the following output:
    > Shutting down ntpd:                      [  OK  ]
    >
    > Starting ntpd:                           [  OK  ]
 
13. `[root@ip-10-10-1-113 ~]#` 
    ```
    ntpdate -u 0.centos.pool.ntp.org
    ```
    You'll see following output:
    > 3 Feb 08:18:04 ntpdate[1252]: adjust time server 123.108.225.6 offset 0.004915 sec
 
14. `[root@ip-10-10-1-113 ~]#` 
    ```
    ntpq -p
    ```
    You'll see the following output:
    ```
    remote           refid      st t when poll reach   delay   offset  jitter
     ==============================================================================
     ns02.hns.net.in 200.98.196.212   2 u   10   64    1   16.674    6.277   0.000
     web10.hnshostin 10.84.87.146     2 u   10   64    1   26.971   -3.804   0.000
     120-88-47-10.in 103.1.106.69     2 u   10   64    1   21.437    3.438   0.000
     ```
 
15. `[root@ip-10-10-1-113 ~]#` 
    ```
    wget http://192.168.2.100/index.html
    ```
    If you're connected to load balancer instance, you can see downloaded `index.html` file.
    
    > --  2014-02-03 08:18:50
    >
    > --  http://192.168.2.100/index.html 
    >
    > Connecting to 192.168.2.100:80... connected.
    >
    > HTTP request sent, awaiting response... 200 OK
    >
    > Length: 16 [text/html]
    >
    > Saving to: “index.html”
    >
    > 100%
    >[=============================================================================================================================>] 
    > 
    > 16 --.-K/s   in 0s      
    >
    > 2014-02-03 08:18:50 (3.43 MB/s) - “index.html” saved [16/16]
    
16. `[root@ip-10-10-1-113 ~]#` 
    ``` 
    nc -z 192.168.2.100 80 
    ```
    Output: 

    > Connection to 192.168.2.100 80 port [tcp/http] succeeded!
 
17. `[root@ip-10-10-1-113 ~]#` 
    ```
    nc -z 192.168.2.103 80
    ```
    Output:

    > Connection to 192.168.2.103 80 port [tcp/http] succeeded!
 
18. `[root@ip-10-10-1-113 ~]#` 
    ``` 
    /etc/init.d/load-balancer-servo restart
    ```
    Output:
    > Stopping load-balancer-servo:  [  OK  ]
    >
    > Starting load-balancer-servo   [  OK  ]

Now, you are connected with load balancer instance of Eucalyptus.
