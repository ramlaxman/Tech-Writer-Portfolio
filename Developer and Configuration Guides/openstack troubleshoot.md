Important Note: Don’t put any # or space before  admin_token. Otherwise Keystone will start to fail.


root@controller:~# gedit /etc/keystone/keystone.conf
root@controller:~# keystone-manage db_sync
root@controller:~# service keystone restart
keystone stop/waiting
keystone start/running, process 5259
root@controller:~# service keystone status
keystone start/running, process 5259
root@controller:~# gedit /etc/keystone/keystone.conf
root@controller:~# export OS_SERVICE_TOKEN=5bdc7674848d94bf499b
root@controller:~# export OS_SERVICE_ENDPOINT=http://controller:35357/v2.0
root@controller:~# keystone tenant-create --name=admin --description="Admin Tenant"
+-------------+----------------------------------+
|   Property  |          	Value           	|
+-------------+----------------------------------+
| description |       	Admin Tenant       	|
|   enabled   |           	True           	|
|  	id 	| c98799486bba4138a5b5d17082733e8d |
| 	name	|          	admin           	|
+-------------+----------------------------------+
root@controller:~# keystone tenant-create --name=service --description="Service Tenant"
+-------------+----------------------------------+
|   Property  |          	Value           	|
+-------------+----------------------------------+
| description |      	Service Tenant      	|
|   enabled   |           	True           	|
|  	id 	| 1a26a0edd0d94618a93cd1ad9527f002 |
| 	name	|         	service          	|
+-------------+----------------------------------+
root@controller:~# keystone user-create --name=admin --pass=cloud123 --email=shripad@clearlogy.com
+----------+----------------------------------+
| Property |          	Value           	|
+----------+----------------------------------+
|  email   |  	shripad@clearlogy.com   	|
| enabled  |           	True           	|
|	id	| cbfed444d5cc44a9815e8e00869dc00a |
|   name   |          	admin           	|
+----------+----------------------------------+
root@controller:~# keystone role-create --name=admin
+----------+----------------------------------+
| Property |          	Value           	|
+----------+----------------------------------+
|	id	| 60b540a4a820458c86498c729b2f0324 |
|   name   |          	admin           	|
+----------+----------------------------------+
root@controller:~# keystone user-role-add --user=admin --tenant=admin --role=admin
root@controller:~# keystone service-create --name=keystone --type=identity --description="Keystone Identity Service"
+-------------+----------------------------------+
|   Property  |          	Value           	|
+-------------+----------------------------------+
| description |	Keystone Identity Service 	|
|  	id 	| 0505e7233deb4a1a8b414db0348527b8 |
| 	name	|         	keystone         	|
| 	type	|         	identity         	|
+-------------+----------------------------------+
root@controller:~# keystone endpoint-create --service-id=0505e7233deb4a1a8b414db0348527b8 --publicurl=http://controller:5000/v2.0 --internalurl=http://controller:5000/v2.0 --adminurl=http://controller:35357/v2.0
+-------------+----------------------------------+
|   Property  |          	Value           	|
+-------------+----------------------------------+
|   adminurl  |   http://controller:35357/v2.0   |
|  	id 	| c0f4b30583254310b25ce8f4c9b8da25 |
| internalurl |   http://controller:5000/v2.0	|
|  publicurl  |   http://controller:5000/v2.0	|
|	region   |        	regionOne         	|
|  service_id | 0505e7233deb4a1a8b414db0348527b8 |
+-------------+----------------------------------+
root@controller:~#







cloud@controller:~$ unset OS_SERVICE_TOKEN OS_SERVICE_ENDPOINT
cloud@controller:~$ clear

cloud@controller:~$ keystone --os-username=admin --os-password=cloud123 --os-auth-url=http://controller:35357/v2.0 token-get
+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Property |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    	Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     	|
+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| expires  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             	2014-04-09T13:03:04Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             	|
|	id	| MIIC8QYJKoZIhvcNAQcCoIIC4jCCAt4CAQExCTAHBgUrDgMCGjCCAUcGCSqGSIb3DQEHAaCCATgEggE0eyJhY2Nlc3MiOiB7InRva2VuIjogeyJpc3N1ZWRfYXQiOiAiMjAxNC0wNC0wOFQxMzowMzowNC4xOTI0MDQiLCAiZXhwaXJlcyI6ICIyMDE0LTA0LTA5VDEzOjAzOjA0WiIsICJpZCI6ICJwbGFjZWhvbGRlciJ9LCAic2VydmljZUNhdGFsb2ciOiBbXSwgInVzZXIiOiB7InVzZXJuYW1lIjogImFkbWluIiwgInJvbGVzX2xpbmtzIjogW10sICJpZCI6ICJjYmZlZDQ0NGQ1Y2M0NGE5ODE1ZThlMDA4NjlkYzAwYSIsICJyb2xlcyI6IFtdLCAibmFtZSI6ICJhZG1pbiJ9LCAibWV0YWRhdGEiOiB7ImlzX2FkbWluIjogMCwgInJvbGVzIjogW119fX0xggGBMIIBfQIBATBcMFcxCzAJBgNVBAYTAlVTMQ4wDAYDVQQIDAVVbnNldDEOMAwGA1UEBwwFVW5zZXQxDjAMBgNVBAoMBVVuc2V0MRgwFgYDVQQDDA93d3cuZXhhbXBsZS5jb20CAQEwBwYFKw4DAhowDQYJKoZIhvcNAQEBBQAEggEAH2JDEa0adg6Faxqr08tUUFdF9OUg3tzepis8RH9DUwBPFpYJ96ZuuXsjinkcN6arIuybHulphE8wPPk2lrhTCn3STS0Eofe81HV1pQnGyAl4xI7eoNmop7kG16xUZTWlAbhZOEKmAFlnsnIVb+liQ+QeSLjfH57Aot0002nQYgdX91BumhE-hQXH3XYs2Y7xT3dr3R0uxbhT0+zkVWKFbJpoBy544KSpEo7edurFaB0K41glWNRDD4E1t35eMcWhexOpR29y7C6A+HPXHD7ofOspE-rQ2fvjA-kKg20C7s0Lk2DRVxvcGpQ1ORh7LeO4IBP-E81eV3FVHZ8TNB9i6g== |
| user_id  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       	cbfed444d5cc44a9815e8e00869dc00a                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       	|
+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


cloud@controller:~$ keystone --os-username=admin --os-password=cloud123 --os-tenant-name=admin --os-auth-url=http://controller:35357/v2.0 token-get
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|  Property |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              	Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               	|
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|  expires  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       	2014-04-09T13:05:05Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       	|
| 	id	| MIIEsgYJKoZIhvcNAQcCoIIEozCCBJ8CAQExCTAHBgUrDgMCGjCCAwgGCSqGSIb3DQEHAaCCAvkEggL1eyJhY2Nlc3MiOiB7InRva2VuIjogeyJpc3N1ZWRfYXQiOiAiMjAxNC0wNC0wOFQxMzowNTowNS4zNDE4NTkiLCAiZXhwaXJlcyI6ICIyMDE0LTA0LTA5VDEzOjA1OjA1WiIsICJpZCI6ICJwbGFjZWhvbGRlciIsICJ0ZW5hbnQiOiB7ImRlc2NyaXB0aW9uIjogIkFkbWluIFRlbmFudCIsICJlbmFibGVkIjogdHJ1ZSwgImlkIjogImM5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgIm5hbWUiOiAiYWRtaW4ifX0sICJzZXJ2aWNlQ2F0YWxvZyI6IFt7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjM1MzU3L3YyLjAiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo1MDAwL3YyLjAiLCAiaWQiOiAiYjM1NmU2MWI1NThiNGVlM2E5NjU3MmY5NzdhMWM1NDAiLCAicHVibGljVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjUwMDAvdjIuMCJ9XSwgImVuZHBvaW50c19saW5rcyI6IFtdLCAidHlwZSI6ICJpZGVudGl0eSIsICJuYW1lIjogImtleXN0b25lIn1dLCAidXNlciI6IHsidXNlcm5hbWUiOiAiYWRtaW4iLCAicm9sZXNfbGlua3MiOiBbXSwgImlkIjogImNiZmVkNDQ0ZDVjYzQ0YTk4MTVlOGUwMDg2OWRjMDBhIiwgInJvbGVzIjogW3sibmFtZSI6ICJhZG1pbiJ9XSwgIm5hbWUiOiAiYWRtaW4ifSwgIm1ldGFkYXRhIjogeyJpc19hZG1pbiI6IDAsICJyb2xlcyI6IFsiNjBiNTQwYTRhODIwNDU4Yzg2NDk4YzcyOWIyZjAzMjQiXX19fTGCAYEwggF9AgEBMFwwVzELMAkGA1UEBhMCVVMxDjAMBgNVBAgMBVVuc2V0MQ4wDAYDVQQHDAVVbnNldDEOMAwGA1UECgwFVW5zZXQxGDAWBgNVBAMMD3d3dy5leGFtcGxlLmNvbQIBATAHBgUrDgMCGjANBgkqhkiG9w0BAQEFAASCAQBtfC0Ag5JqqGLq7r08DZKLLvkFg+OUxYw4wQUifT8ZbMHzS5OWnggebDzcWufiH3G5zkdKSD7qPipv4GKaj0BBIlJBmUufb7ZSkfCNh2Un8mBegOACmtx0jDOvlhVEE7-YcTQ2Crlr1ulN4m456VgnB7YtpaqOBQBPmwzyvu5jRu3aESsKeCRrd5FGCk-zU2kZ-vGR9PPJKYq02xhAxmbFqn2-yiNaQsIiFQB7h7DzrHHrqYca7Bm35+q5zHGeCPUpmUV3yYRnIHCXyRqBnqbAuOXGmtzHDmuCKrbnZyAlA63sgBXIRcuB10iGyAP80jeBDxtpt6By7SthHGkdo4QU |
| tenant_id |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 	c98799486bba4138a5b5d17082733e8d                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 	|
|  user_id  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 	cbfed444d5cc44a9815e8e00869dc00a                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 	|
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
cloud@controller:~$ touch openrx.sh
cloud@controller:~$ gedit openrx.sh
cloud@controller:~$ rm openrx.sh
cloud@controller:~$ ls
Desktop  Documents  Downloads  examples.desktop  Music  Pictures  Public  Templates  Videos
cloud@controller:~$ touch openrc.sh
cloud@controller:~$ gedit openrc.sh
cloud@controller:~$ source openrc.sh
cloud@controller:~$ keystone token-get
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|  Property |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              	Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               	|
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|  expires  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       	2014-04-09T13:07:26Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       	|
| 	id	| MIIEsgYJKoZIhvcNAQcCoIIEozCCBJ8CAQExCTAHBgUrDgMCGjCCAwgGCSqGSIb3DQEHAaCCAvkEggL1eyJhY2Nlc3MiOiB7InRva2VuIjogeyJpc3N1ZWRfYXQiOiAiMjAxNC0wNC0wOFQxMzowNzoyNi4wNzQ4MTQiLCAiZXhwaXJlcyI6ICIyMDE0LTA0LTA5VDEzOjA3OjI2WiIsICJpZCI6ICJwbGFjZWhvbGRlciIsICJ0ZW5hbnQiOiB7ImRlc2NyaXB0aW9uIjogIkFkbWluIFRlbmFudCIsICJlbmFibGVkIjogdHJ1ZSwgImlkIjogImM5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgIm5hbWUiOiAiYWRtaW4ifX0sICJzZXJ2aWNlQ2F0YWxvZyI6IFt7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjM1MzU3L3YyLjAiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo1MDAwL3YyLjAiLCAiaWQiOiAiYjM1NmU2MWI1NThiNGVlM2E5NjU3MmY5NzdhMWM1NDAiLCAicHVibGljVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjUwMDAvdjIuMCJ9XSwgImVuZHBvaW50c19saW5rcyI6IFtdLCAidHlwZSI6ICJpZGVudGl0eSIsICJuYW1lIjogImtleXN0b25lIn1dLCAidXNlciI6IHsidXNlcm5hbWUiOiAiYWRtaW4iLCAicm9sZXNfbGlua3MiOiBbXSwgImlkIjogImNiZmVkNDQ0ZDVjYzQ0YTk4MTVlOGUwMDg2OWRjMDBhIiwgInJvbGVzIjogW3sibmFtZSI6ICJhZG1pbiJ9XSwgIm5hbWUiOiAiYWRtaW4ifSwgIm1ldGFkYXRhIjogeyJpc19hZG1pbiI6IDAsICJyb2xlcyI6IFsiNjBiNTQwYTRhODIwNDU4Yzg2NDk4YzcyOWIyZjAzMjQiXX19fTGCAYEwggF9AgEBMFwwVzELMAkGA1UEBhMCVVMxDjAMBgNVBAgMBVVuc2V0MQ4wDAYDVQQHDAVVbnNldDEOMAwGA1UECgwFVW5zZXQxGDAWBgNVBAMMD3d3dy5leGFtcGxlLmNvbQIBATAHBgUrDgMCGjANBgkqhkiG9w0BAQEFAASCAQClKd06dE1SFZDz-PH53m1QRezwJo+iE+xJIx4YdCzd17id6FBCMDferLaIIUg1+yxldPIyk2UhZP+dSB6S+t6gfC-YmLyap-62RvhjNLnPnzccmylck+wvjZuxREh4-nyfKEV7IhDGmyLpLZX6SVzxpJE46lXPxmrC-d9+xa3DxSGx+p088v1EX280aMPy6RycDJGAtl4tqNm-Cl1faJ-WttUsSzyfJsjarUg+0jizIvtd6NncWyk8naA15rHYQpmQEwxqaIGO9Kg1vvMmYlVTjX3XPy8bssuAEpJFUQkIcdet2-oGD2wKbTZppLfDpDHpl5ZzIUhk+yQnCrdyF3Jh |
| tenant_id |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 	c98799486bba4138a5b5d17082733e8d                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 	|
|  user_id  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 	cbfed444d5cc44a9815e8e00869dc00a                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 	|
+-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

cloud@controller:~$ keystone user-list
+----------------------------------+-------+---------+-----------------------+
|            	id            	|  name | enabled |     	email     	|
+----------------------------------+-------+---------+-----------------------+
| cbfed444d5cc44a9815e8e00869dc00a | admin |   True  | shripad@clearlogy.com |
+----------------------------------+-------+---------+-----------------------+






















Glance Installation
root@controller:~# gedit /etc/glance/glance-api.conf
root@controller:~# gedit /etc/glance/glance-registry.conf
root@controller:~# cd /var/lib/glance/
root@controller:/var/lib/glance# ls
glance.sqlite  image-cache  images
root@controller:/var/lib/glance# rm glance.sqlite

root@controller:~# mysql -u root -p
Enter password:

mysql> CREATE DATABASE glance;
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON glance.* TO 'glance'@'localhost' IDENTIFIED BY 'cloud123';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON glance.* TO 'glance'@'%' IDENTIFIED BY 'cloud123';
Query OK, 0 rows affected (0.00 sec)

mysql> quit
Bye
root@controller:~# glance-manage db_sync
root@controller:~# cd /home/cloud/
root@controller:~# source openrc.sh
root@controller:~# keystone user-create --name=glance --pass=cloud123 --email=shripad@clearlogy.com
+----------+----------------------------------+
| Property |          	Value           	|
+----------+----------------------------------+
|  email   |  	shripad@clearlogy.com   	|
| enabled  |           	True           	|
|	id	| e9348e80233147e584e327e5a6dea5bf |
|   name   |          	glance          	|
+----------+----------------------------------+

root@controller:~# keystone user-role-add --user=glance --tenant=service --role=admin
root@controller:~# gedit /etc/glance/glance-api.conf
root@controller:~# gedit /etc/glance/glance-registry.conf
root@controller:~# gedit  /etc/glance/glance-api-paste.ini
root@controller:~# gedit /etc/glance/glance-registry-paste.ini
root@controller:~# keystone service-create --name=glance --type=image --description="Glance Image Service"
+-------------+----------------------------------+
|   Property  |          	Value           	|
+-------------+----------------------------------+
| description |   	Glance Image Service   	|
|  	id 	| 6df4ba2a2c034737922a5a27553ff9fc |
| 	name	|          	glance          	|
| 	type	|          	image           	|
+-------------+----------------------------------+
root@controller:~# keystone endpoint-create --service-id=6df4ba2a2c034737922a5a27553ff9fc --publicurl=http://controller:9292 --internalurl=http://controller:9292 --adminurl=http://controller:9292
+-------------+----------------------------------+
|   Property  |          	Value           	|
+-------------+----------------------------------+
|   adminurl  |  	http://controller:9292  	|
|  	id 	| 6e77e12545ba40df89976c46dad5cb28 |
| internalurl |  	http://controller:9292  	|
|  publicurl  |  	http://controller:9292  	|
|	region   |        	regionOne         	|
|  service_id | 6df4ba2a2c034737922a5a27553ff9fc |
+-------------+----------------------------------+
root@controller:~# service glance-registry restart
glance-registry stop/waiting
glance-registry start/running, process 6695
root@controller:~# service glance-api restart
glance-api stop/waiting
glance-api start/running, process 6708

root@controller:~/images# glance image-create --name="CirrOS 0.3.1" --disk-format=qcow2 --container-format=bare --is-public=true < cirros-0.3.1-x86_64-disk.img
You must provide a username via either --os-username or env[OS_USERNAME]











root@controller:~/images# cd /home/cloud/
root@controller:~# source openrc.sh
root@controller:~# source openrc.sh
root@controller:~# cd /home/cloud/images/
root@controller:~/images# glance image-create --name="CirrOS 0.3.1" --disk-format=qcow2 --container-format=bare --is-public=true < cirros-0.3.1-x86_64-disk.img
+------------------+--------------------------------------+
| Property     	| Value                            	|
+------------------+--------------------------------------+
| checksum     	| d972013792949d0d3ba628fbe8685bce 	|
| container_format | bare                             	|
| created_at   	| 2014-04-08T13:48:29              	|
| deleted      	| False                            	|
| deleted_at   	| None                             	|
| disk_format  	| qcow2                            	|
| id           	| fbcbc4bd-6cd2-4dd7-986a-6d660c2551a7 |
| is_public    	| True                             	|
| min_disk     	| 0                                	|
| min_ram      	| 0                                	|
| name         	| CirrOS 0.3.1                     	|
| owner        	| c98799486bba4138a5b5d17082733e8d 	|
| protected    	| False                            	|
| size         	| 13147648                         	|
| status       	| active                           	|
| updated_at   	| 2014-04-08T13:48:30              	|
+------------------+--------------------------------------+

root@controller:~/images# glance image-list
+--------------------------------------+--------------+-------------+------------------+----------+--------+
| ID                               	| Name     	| Disk Format | Container Format | Size 	| Status |
+--------------------------------------+--------------+-------------+------------------+----------+--------+
| fbcbc4bd-6cd2-4dd7-986a-6d660c2551a7 | CirrOS 0.3.1 | qcow2   	| bare         	| 13147648 | active |
+--------------------------------------+--------------+-------------+------------------+----------+--------+










CONFIGURE THE COMPUTE NODE
root@controller:~# nova-manage db sync
2014-04-09 11:40:35.944 6007 INFO migrate.versioning.api [-] 132 -> 133... 
2014-04-09 11:41:00.600 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:00.600 6007 INFO migrate.versioning.api [-] 133 -> 134... 
2014-04-09 11:41:01.185 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:01.185 6007 INFO migrate.versioning.api [-] 134 -> 135... 
2014-04-09 11:41:01.487 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:01.487 6007 INFO migrate.versioning.api [-] 135 -> 136... 
2014-04-09 11:41:01.789 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:01.789 6007 INFO migrate.versioning.api [-] 136 -> 137... 
2014-04-09 11:41:02.048 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:02.048 6007 INFO migrate.versioning.api [-] 137 -> 138... 
2014-04-09 11:41:02.333 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:02.333 6007 INFO migrate.versioning.api [-] 138 -> 139... 
2014-04-09 11:41:02.584 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:02.585 6007 INFO migrate.versioning.api [-] 139 -> 140... 
2014-04-09 11:41:02.666 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:02.666 6007 INFO migrate.versioning.api [-] 140 -> 141... 
2014-04-09 11:41:02.977 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:02.978 6007 INFO migrate.versioning.api [-] 141 -> 142... 
2014-04-09 11:41:03.229 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:03.229 6007 INFO migrate.versioning.api [-] 142 -> 143... 
2014-04-09 11:41:03.665 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:03.665 6007 INFO migrate.versioning.api [-] 143 -> 144... 
2014-04-09 11:41:04.717 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:04.718 6007 INFO migrate.versioning.api [-] 144 -> 145... 
2014-04-09 11:41:04.894 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:04.894 6007 INFO migrate.versioning.api [-] 145 -> 146... 
2014-04-09 11:41:05.187 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:05.187 6007 INFO migrate.versioning.api [-] 146 -> 147... 
2014-04-09 11:41:05.513 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:05.514 6007 INFO migrate.versioning.api [-] 147 -> 148... 
2014-04-09 11:41:06.401 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:06.401 6007 INFO migrate.versioning.api [-] 148 -> 149... 
2014-04-09 11:41:12.116 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:12.116 6007 INFO migrate.versioning.api [-] 149 -> 150... 
2014-04-09 11:41:12.767 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:12.768 6007 INFO migrate.versioning.api [-] 150 -> 151... 
2014-04-09 11:41:13.321 6007 INFO migrate.versioning.api [-] done
2014-04-09 11:41:13.321 6007 INFO migrate.versioning.api [-] 151 -> 152... 
root@controller:~# gedit /etc/nova/nova.conf
root@controller:~# keystone user-create --name=nova --pass=cloud123 --email=shripad@clearlogy.com
Expecting an auth URL via either --os-auth-url or env[OS_AUTH_URL]
root@controller:~# cd /home/cloud/
root@controller:~# source openrc.sh
root@controller:~# keystone user-create --name=nova --pass=cloud123 --email=shripad@clearlogy.com
+----------+----------------------------------+
| Property |              Value               |
+----------+----------------------------------+
|  email   |      shripad@clearlogy.com       |
| enabled  |               True               |
|    id    | 35a54a8d4bc14b3390b4afa8b220bc51 |
|   name   |               nova               |
+----------+----------------------------------+
root@controller:~# keystone user-role-add --user=nova --tenant=service --role=admin
root@controller:~# gedit /etc/nova/nova.conf
^C
root@controller:~# gedit /etc/nova/api-paste.ini
root@controller:~# gedit /etc/nova/nova.conf
root@controller:~# keystone service-create --name=nova --type=compute --description="Nova Compute service"
+-------------+----------------------------------+
|   Property  |              Value               |
+-------------+----------------------------------+
| description |       Nova Compute service       |
|      id     | 96287ac914734ee5b93d66a43d01423b |
|     name    |               nova               |
|     type    |             compute              |
+-------------+----------------------------------+
root@controller:~# keystone endpoint-create --service-id=96287ac914734ee5b93d66a43d01423b --publicurl=http://controller:8774/v2/%\(tenant_id\)s --internalurl=http://controller:8774/v2/%\(tenant_id\)s --adminurl=http://controller:8774/v2/%\(tenant_id\)s
+-------------+-----------------------------------------+
|   Property  |                  Value                  |
+-------------+-----------------------------------------+
|   adminurl  | http://controller:8774/v2/%(tenant_id)s |
|      id     |     0833686a32024dc3ba7c62b75cb28d00    |
| internalurl | http://controller:8774/v2/%(tenant_id)s |
|  publicurl  | http://controller:8774/v2/%(tenant_id)s |
|    region   |                regionOne                |
|  service_id |     96287ac914734ee5b93d66a43d01423b    |
+-------------+-----------------------------------------+
root@controller:~# service nova-api restart
nova-api stop/waiting
nova-api start/running, process 6315
root@controller:~# service nova-cert restart
nova-cert stop/waiting
nova-cert start/running, process 6340
root@controller:~# service nova-consoleauth restart
nova-consoleauth stop/waiting
nova-consoleauth start/running, process 6362
root@controller:~# service nova-scheduler restart
nova-scheduler stop/waiting
nova-scheduler start/running, process 6387
root@controller:~# service nova-conductor restart
nova-conductor stop/waiting
nova-conductor start/running, process 6411
root@controller:~# service nova-novncproxy restart
nova-novncproxy stop/waiting
nova-novncproxy start/running, process 6435
root@controller:~# nova image-list
+--------------------------------------+--------------+--------+--------+
| ID                                                  | Name           | Status | Server |
+--------------------------------------+--------------+--------+--------+
| fbcbc4bd-6cd2-4dd7-986a-6d660c2551a7 | CirrOS 0.3.1 | ACTIVE |        |
+--------------------------------------+--------------+--------+--------+





















The local_settings.py file as like follows:

http://fpaste.org/94869/


root@controller:~# /usr/share/openstack-dashboard/manage.py syncdb
Creating tables ...
Creating table django_content_type
Creating table auth_permission
Creating table auth_group_permissions
Creating table auth_group
Creating table auth_user_groups
Creating table auth_user_user_permissions
Creating table auth_user
Creating table django_session

You just installed Django's auth system, which means you don't have any superusers defined.
Would you like to create one now? (yes/no): yes
Username (leave blank to use 'root'):
Email address: shripad@clearlogy.com
Password:
Password (again):
Superuser created successfully.
Installing custom SQL ...
Installing indexes ...
Installed 0 object(s) from 0 fixture(s)
root@controller:~#




















Openstack API Requests
cloud@controller:~$ curl -i 'http://controller:5000/v2.0/tokens' -X POST -H "Content-Type: application/json" -H "Accept: application/json"  -d '{"auth": {"tenantName": "admin", "passwordCredentials": {"username": "admin", "password": "cloud123"}}}'
HTTP/1.1 200 OK
Vary: X-Auth-Token
Content-Type: application/json
Content-Length: 5552
Date: Thu, 10 Apr 2014 13:02:03 GMT

{"access": {"token": {"issued_at": "2014-04-10T13:02:03.738432", "expires": "2014-04-11T13:02:03Z", "id": "MIIKDAYJKoZIhvcNAQcCoIIJ-TCCCfkCAQExCTAHBgUrDgMCGjCCCGIGCSqGSIb3DQEHAaCCCFMEgghPeyJhY2Nlc3MiOiB7InRva2VuIjogeyJpc3N1ZWRfYXQiOiAiMjAxNC0wNC0xMFQxMzowMjowMy43Mzg0MzIiLCAiZXhwaXJlcyI6ICIyMDE0LTA0LTExVDEzOjAyOjAzWiIsICJpZCI6ICJwbGFjZWhvbGRlciIsICJ0ZW5hbnQiOiB7ImRlc2NyaXB0aW9uIjogIkFkbWluIFRlbmFudCIsICJlbmFibGVkIjogdHJ1ZSwgImlkIjogImM5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgIm5hbWUiOiAiYWRtaW4ifX0sICJzZXJ2aWNlQ2F0YWxvZyI6IFt7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzYvdjEvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgImlkIjogIjBmNTVlMWZjZmE0NDQ2MjNhMGNjZTRlNDMwZDJmZTNjIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogInZvbHVtZSIsICJuYW1lIjogImNpbmRlciJ9LCB7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjkyOTIiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIiwgImlkIjogImI2ODcxNjU3NmRhODQ2Njc4ZTg4NDg4NWExMmJiMTdhIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImltYWdlIiwgIm5hbWUiOiAiZ2xhbmNlIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3NC92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAiaWQiOiAiYzY5M2E2OGU5ODM0NGE4Yjg5NzY1MzFmYjhmMGE2MGIiLCAicHVibGljVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQifV0sICJlbmRwb2ludHNfbGlua3MiOiBbXSwgInR5cGUiOiAiY29tcHV0ZSIsICJuYW1lIjogIm5vdmEifSwgeyJlbmRwb2ludHMiOiBbeyJhZG1pblVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YyL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgInJlZ2lvbiI6ICJyZWdpb25PbmUiLCAiaW50ZXJuYWxVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJpZCI6ICIxYzU5ZjkwMGVhOTA0Nzc3ODEyNGM2NWYwODk1ZGFmZSIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCJ9XSwgImVuZHBvaW50c19saW5rcyI6IFtdLCAidHlwZSI6ICJ2b2x1bWV2MiIsICJuYW1lIjogImNpbmRlcnYyIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6MzUzNTcvdjIuMCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjUwMDAvdjIuMCIsICJpZCI6ICJiMzU2ZTYxYjU1OGI0ZWUzYTk2NTcyZjk3N2ExYzU0MCIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6NTAwMC92Mi4wIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImlkZW50aXR5IiwgIm5hbWUiOiAia2V5c3RvbmUifV0sICJ1c2VyIjogeyJ1c2VybmFtZSI6ICJhZG1pbiIsICJyb2xlc19saW5rcyI6IFtdLCAiaWQiOiAiY2JmZWQ0NDRkNWNjNDRhOTgxNWU4ZTAwODY5ZGMwMGEiLCAicm9sZXMiOiBbeyJuYW1lIjogImFkbWluIn1dLCAibmFtZSI6ICJhZG1pbiJ9LCAibWV0YWRhdGEiOiB7ImlzX2FkbWluIjogMCwgInJvbGVzIjogWyI2MGI1NDBhNGE4MjA0NThjODY0OThjNzI5YjJmMDMyNCJdfX19MYIBgTCCAX0CAQEwXDBXMQswCQYDVQQGEwJVUzEOMAwGA1UECAwFVW5zZXQxDjAMBgNVBAcMBVVuc2V0MQ4wDAYDVQQKDAVVbnNldDEYMBYGA1UEAwwPd3d3LmV4YW1wbGUuY29tAgEBMAcGBSsOAwIaMA0GCSqGSIb3DQEBAQUABIIBAKNEfZpyj6pxH+75ssatEVE-VohITPy9xEmOUg-MnuWN72CwxAtOs1+Kp4vHnaijIkFZPbHENNIgrza7juq+vuThPNj6RAQLnqeXdBfaXQONXHNNQr9dLIon6chKTZj3DDcTrXSMizJWRN5kO+cPS6gJQMk+OG5fB-buU5++ZzJkG7yRw8A3NShs6gJmhlp6ILu4On5DtYeToznhVq21DXUcK5yVZHw0NxpMKDc6mJLe5sD216zBF-UZg98QRP7RDDcP+HArIWuQkZwsV-0pXSFkwfK1gGW3a3dV09jUWXfEjNLXC+Fqy-18W3AIpN6nP3-oG5zpk1zduiL25GommqE=", "tenant": {"description": "Admin Tenant", "enabled": true, "id": "c98799486bba4138a5b5d17082733e8d", "name": "admin"}}, "serviceCatalog": [{"endpoints": [{"adminURL": "http://controller:8776/v1/c98799486bba4138a5b5d17082733e8d", "region": "regionOne", "internalURL": "http://controller:8776/v1/c98799486bba4138a5b5d17082733e8d", "id": "0f55e1fcfa444623a0cce4e430d2fe3c", "publicURL": "http://controller:8776/v1/c98799486bba4138a5b5d17082733e8d"}], "endpoints_links": [], "type": "volume", "name": "cinder"}, {"endpoints": [{"adminURL": "http://controller:9292", "region": "regionOne", "internalURL": "http://controller:9292", "id": "b68716576da846678e884885a12bb17a", "publicURL": "http://controller:9292"}], "endpoints_links": [], "type": "image", "name": "glance"}, {"endpoints": [{"adminURL": "http://controller:8774/v2/c98799486bba4138a5b5d17082733e8d", "region": "regionOne", "internalURL": "http://controller:8774/v2/c98799486bba4138a5b5d17082733e8d", "id": "c693a68e98344a8b8976531fb8f0a60b", "publicURL": "http://controller:8774/v2/c98799486bba4138a5b5d17082733e8d"}], "endpoints_links": [], "type": "compute", "name": "nova"}, {"endpoints": [{"adminURL": "http://controller:8776/v2/c98799486bba4138a5b5d17082733e8d", "region": "regionOne", "internalURL": "http://controller:8776/v2/c98799486bba4138a5b5d17082733e8d", "id": "1c59f900ea9047778124c65f0895dafe", "publicURL": "http://controller:8776/v2/c98799486bba4138a5b5d17082733e8d"}], "endpoints_links": [], "type": "volumev2", "name": "cinderv2"}, {"endpoints": [{"adminURL": "http://controller:35357/v2.0", "region": "regionOne", "internalURL": "http://controller:5000/v2.0", "id": "b356e61b558b4ee3a96572f977a1c540", "publicURL": "http://controller:5000/v2.0"}], "endpoints_links": [], "type": "identity", "name": "keystone"}], "user": {"username": "admin", "roles_links": [], "id": "cbfed444d5cc44a9815e8e00869dc00a", "roles": [{"name": "admin"}], "name": "admin"}, "metadata": {"is_admin": 0, "roles": ["60b540a4a820458c86498c729b2f0324"]}}}


curl -i 'http://controller:5000/v2.0/tokens' -X POST -H "Content-Type: application/json" -H "Accept: application/json"  -d '{"auth": {"tenantName": "admin", "passwordCredentials": {"username": "admin", "password": "cloud123"}}}'


curl -i 'http://controller:5000/v2.0/tokens' -X POST -H "Content-Type: application/json" -H "Accept: application/json" -H "User-Agent: python-keystoneclient" -H "X-Auth-Token: token" -d '{"auth": {"tenantName": "admin", "passwordCredentials": {"username": "admin", "password": "cloud123"}}}'




API requests

1. source the openrc.sh file 

2.  run the following command [Look for values in openrc.sh file ]

curl -i 'http://controller:5000/v2.0/tokens' -X POST -H "Content-Type: application/json" -H "Accept: application/json"  -d '{"auth": {"tenantName": "admin", "passwordCredentials": {"username": "admin", "password": "cloud123"}}}'

The value of Token is id section in the token

HTTP/1.1 200 OK
Vary: X-Auth-Token
Content-Type: application/json
Content-Length: 5552
Date: Thu, 10 Apr 2014 13:41:29 GMT

{"access": {"token": {"issued_at": "2014-04-10T13:41:29.251331", "expires": "2014-04-11T13:41:29Z", "id": "MIIKDAYJKoZIhvcNAQcCoIIJ-TCCCfkCAQExCTAHBgUrDgMCGjCCCGIGCSqGSIb3DQEHAaCCCFMEgghPeyJhY2Nlc3MiOiB7InRva2VuIjogeyJpc3N1ZWRfYXQiOiAiMjAxNC0wNC0xMFQxMzo0MToyOS4yNTEzMzEiLCAiZXhwaXJlcyI6ICIyMDE0LTA0LTExVDEzOjQxOjI5WiIsICJpZCI6ICJwbGFjZWhvbGRlciIsICJ0ZW5hbnQiOiB7ImRlc2NyaXB0aW9uIjogIkFkbWluIFRlbmFudCIsICJlbmFibGVkIjogdHJ1ZSwgImlkIjogImM5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgIm5hbWUiOiAiYWRtaW4ifX0sICJzZXJ2aWNlQ2F0YWxvZyI6IFt7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzYvdjEvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgImlkIjogIjBmNTVlMWZjZmE0NDQ2MjNhMGNjZTRlNDMwZDJmZTNjIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogInZvbHVtZSIsICJuYW1lIjogImNpbmRlciJ9LCB7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjkyOTIiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIiwgImlkIjogImI2ODcxNjU3NmRhODQ2Njc4ZTg4NDg4NWExMmJiMTdhIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImltYWdlIiwgIm5hbWUiOiAiZ2xhbmNlIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3NC92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAiaWQiOiAiYzY5M2E2OGU5ODM0NGE4Yjg5NzY1MzFmYjhmMGE2MGIiLCAicHVibGljVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQifV0sICJlbmRwb2ludHNfbGlua3MiOiBbXSwgInR5cGUiOiAiY29tcHV0ZSIsICJuYW1lIjogIm5vdmEifSwgeyJlbmRwb2ludHMiOiBbeyJhZG1pblVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YyL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgInJlZ2lvbiI6ICJyZWdpb25PbmUiLCAiaW50ZXJuYWxVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJpZCI6ICIxYzU5ZjkwMGVhOTA0Nzc3ODEyNGM2NWYwODk1ZGFmZSIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCJ9XSwgImVuZHBvaW50c19saW5rcyI6IFtdLCAidHlwZSI6ICJ2b2x1bWV2MiIsICJuYW1lIjogImNpbmRlcnYyIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6MzUzNTcvdjIuMCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjUwMDAvdjIuMCIsICJpZCI6ICJiMzU2ZTYxYjU1OGI0ZWUzYTk2NTcyZjk3N2ExYzU0MCIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6NTAwMC92Mi4wIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImlkZW50aXR5IiwgIm5hbWUiOiAia2V5c3RvbmUifV0sICJ1c2VyIjogeyJ1c2VybmFtZSI6ICJhZG1pbiIsICJyb2xlc19saW5rcyI6IFtdLCAiaWQiOiAiY2JmZWQ0NDRkNWNjNDRhOTgxNWU4ZTAwODY5ZGMwMGEiLCAicm9sZXMiOiBbeyJuYW1lIjogImFkbWluIn1dLCAibmFtZSI6ICJhZG1pbiJ9LCAibWV0YWRhdGEiOiB7ImlzX2FkbWluIjogMCwgInJvbGVzIjogWyI2MGI1NDBhNGE4MjA0NThjODY0OThjNzI5YjJmMDMyNCJdfX19MYIBgTCCAX0CAQEwXDBXMQswCQYDVQQGEwJVUzEOMAwGA1UECAwFVW5zZXQxDjAMBgNVBAcMBVVuc2V0MQ4wDAYDVQQKDAVVbnNldDEYMBYGA1UEAwwPd3d3LmV4YW1wbGUuY29tAgEBMAcGBSsOAwIaMA0GCSqGSIb3DQEBAQUABIIBAJBS948FZkIzdg46mAf5Qly0z0fuXdCYPlACFNPxKzbGBGZHcy1UfuKhKmMUlVCS2HAx3UxEiGZPnI4KlqG+uIRQpzGy6HOLBEn2j+QOO76lfV-lYsbIBdlcRmfeMI8Lx+Z546UIeqNt8cmJWJNhKYnR45ydxt6L2nAqFPGuxPDuc5p04kaNg0RQ6kM2EAQWTrMAE0WPiaiNb0h4TM8N+mQHfl9fGctG09m9HG69os8mMFjddSB335WrPXSpHiHJHOJpKizEHsZ229poETtlVe4NGnvi6gGzGzPyQfGg+Lzq1tGMa6Wbiy2WVq2Z2matSLhVfn1lxJU+z7jQnGW18NE=", "tenant": {"description": "Admin Tenant", "enabled": true, "id": "c98799486bba4138a5b5d17082733e8d", "name": "admin"}}, "serviceCatalog": [{"endpoints": [{"adminURL": "http://controller:8776/v1/c98799486bba4138a5b5d17082733e8d", "region": "regionOne", "internalURL": "http://controller:8776/v1/c98799486bba4138a5b5d17082733e8d", "id": "0f55e1fcfa444623a0cce4e430d2fe3c", "publicURL": "http://controller:8776/v1/c98799486bba4138a5b5d17082733e8d"}], "endpoints_links": [], "type": "volume", "name": "cinder"}, {"endpoints": [{"adminURL": "http://controller:9292", "region": "regionOne", "internalURL": "http://controller:9292", "id": "b68716576da846678e884885a12bb17a", "publicURL": "http://controller:9292"}], "endpoints_links": [], "type": "image", "name": "glance"}, {"endpoints": [{"adminURL": "http://controller:8774/v2/c98799486bba4138a5b5d17082733e8d", "region": "regionOne", "internalURL": "http://controller:8774/v2/c98799486bba4138a5b5d17082733e8d", "id": "c693a68e98344a8b8976531fb8f0a60b", "publicURL": "http://controller:8774/v2/c98799486bba4138a5b5d17082733e8d"}], "endpoints_links": [], "type": "compute", "name": "nova"}, {"endpoints": [{"adminURL": "http://controller:8776/v2/c98799486bba4138a5b5d17082733e8d", "region": "regionOne", "internalURL": "http://controller:8776/v2/c98799486bba4138a5b5d17082733e8d", "id": "1c59f900ea9047778124c65f0895dafe", "publicURL": "http://controller:8776/v2/c98799486bba4138a5b5d17082733e8d"}], "endpoints_links": [], "type": "volumev2", "name": "cinderv2"}, {"endpoints": [{"adminURL": "http://controller:35357/v2.0", "region": "regionOne", "internalURL": "http://controller:5000/v2.0", "id": "b356e61b558b4ee3a96572f977a1c540", "publicURL": "http://controller:5000/v2.0"}], "endpoints_links": [], "type": "identity", "name": "keystone"}], "user": {"username": "admin", "roles_links": [], "id": "cbfed444d5cc44a9815e8e00869dc00a", "roles": [{"name": "admin"}], "name": "admin"}, "metadata": {"is_admin": 0, "roles": ["60b540a4a820458c86498c729b2f0324"]}}}cloud@contro" -H "Accept: application/json"  -d '{"auth": {"tenantName": "admin", "passwordCredentials": {"username": "admin", "password": "cloud123"}}}'


3. To check for the image service API requests, use this token as input……… 

   As shown below









cloud@controller:~$ curl -i -X GET http://controller:35357/v2.0/tenants -H "User-Agent: python-keystoneclient" -H "X-Auth-Token: MIIKDAYJKoZIhvcNAQcCoIIJ-TCCCfkCAQExCTAHBgUrDgMCGjCCCGIGCSqGSIb3DQEHAaCCCFMEgghPeyJhY2Nlc3MiOiB7InRva2VuIjogeyJpc3N1ZWRfYXQiOiAiMjAxNC0wNC0xMFQxMzo0MToyOS4yNTEzMzEiLCAiZXhwaXJlcyI6ICIyMDE0LTA0LTExVDEzOjQxOjI5WiIsICJpZCI6ICJwbGFjZWhvbGRlciIsICJ0ZW5hbnQiOiB7ImRlc2NyaXB0aW9uIjogIkFkbWluIFRlbmFudCIsICJlbmFibGVkIjogdHJ1ZSwgImlkIjogImM5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgIm5hbWUiOiAiYWRtaW4ifX0sICJzZXJ2aWNlQ2F0YWxvZyI6IFt7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzYvdjEvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgImlkIjogIjBmNTVlMWZjZmE0NDQ2MjNhMGNjZTRlNDMwZDJmZTNjIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogInZvbHVtZSIsICJuYW1lIjogImNpbmRlciJ9LCB7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjkyOTIiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIiwgImlkIjogImI2ODcxNjU3NmRhODQ2Njc4ZTg4NDg4NWExMmJiMTdhIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImltYWdlIiwgIm5hbWUiOiAiZ2xhbmNlIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3NC92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAiaWQiOiAiYzY5M2E2OGU5ODM0NGE4Yjg5NzY1MzFmYjhmMGE2MGIiLCAicHVibGljVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQifV0sICJlbmRwb2ludHNfbGlua3MiOiBbXSwgInR5cGUiOiAiY29tcHV0ZSIsICJuYW1lIjogIm5vdmEifSwgeyJlbmRwb2ludHMiOiBbeyJhZG1pblVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YyL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgInJlZ2lvbiI6ICJyZWdpb25PbmUiLCAiaW50ZXJuYWxVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJpZCI6ICIxYzU5ZjkwMGVhOTA0Nzc3ODEyNGM2NWYwODk1ZGFmZSIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCJ9XSwgImVuZHBvaW50c19saW5rcyI6IFtdLCAidHlwZSI6ICJ2b2x1bWV2MiIsICJuYW1lIjogImNpbmRlcnYyIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6MzUzNTcvdjIuMCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjUwMDAvdjIuMCIsICJpZCI6ICJiMzU2ZTYxYjU1OGI0ZWUzYTk2NTcyZjk3N2ExYzU0MCIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6NTAwMC92Mi4wIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImlkZW50aXR5IiwgIm5hbWUiOiAia2V5c3RvbmUifV0sICJ1c2VyIjogeyJ1c2VybmFtZSI6ICJhZG1pbiIsICJyb2xlc19saW5rcyI6IFtdLCAiaWQiOiAiY2JmZWQ0NDRkNWNjNDRhOTgxNWU4ZTAwODY5ZGMwMGEiLCAicm9sZXMiOiBbeyJuYW1lIjogImFkbWluIn1dLCAibmFtZSI6ICJhZG1pbiJ9LCAibWV0YWRhdGEiOiB7ImlzX2FkbWluIjogMCwgInJvbGVzIjogWyI2MGI1NDBhNGE4MjA0NThjODY0OThjNzI5YjJmMDMyNCJdfX19MYIBgTCCAX0CAQEwXDBXMQswCQYDVQQGEwJVUzEOMAwGA1UECAwFVW5zZXQxDjAMBgNVBAcMBVVuc2V0MQ4wDAYDVQQKDAVVbnNldDEYMBYGA1UEAwwPd3d3LmV4YW1wbGUuY29tAgEBMAcGBSsOAwIaMA0GCSqGSIb3DQEBAQUABIIBAJBS948FZkIzdg46mAf5Qly0z0fuXdCYPlACFNPxKzbGBGZHcy1UfuKhKmMUlVCS2HAx3UxEiGZPnI4KlqG+uIRQpzGy6HOLBEn2j+QOO76lfV-lYsbIBdlcRmfeMI8Lx+Z546UIeqNt8cmJWJNhKYnR45ydxt6L2nAqFPGuxPDuc5p04kaNg0RQ6kM2EAQWTrMAE0WPiaiNb0h4TM8N+mQHfl9fGctG09m9HG69os8mMFjddSB335WrPXSpHiHJHOJpKizEHsZ229poETtlVe4NGnvi6gGzGzPyQfGg+Lzq1tGMa6Wbiy2WVq2Z2matSLhVfn1lxJU+z7jQnGW18NE="



##############################
The output is 

HTTP/1.1 200 OK
Vary: X-Auth-Token
Content-Type: application/json
Content-Length: 256
Date: Thu, 10 Apr 2014 13:43:35 GMT

{"tenants_links": [], "tenants": [{"description": "Service Tenant", "enabled": true, "id": "1a26a0edd0d94618a93cd1ad9527f002", "name": "service"}, {"description": "Admin Tenant", "enabled": true, "id": "c98799486bba4138a5b5d17082733e8d", "name": "admin"}]}



3. For getting endpoint

cloud@controller:~$ curl -i -X GET http://controller:35357/v2.0/endpoints -H "User-Agent: python-keystoneclient" -H "X-Auth-Token: MIIKDAYJKoZIhvcNAQcCoIIJ-TCCCfkCAQExCTAHBgUrDgMCGjCCCGIGCSqGSIb3DQEHAaCCCFMEgghPeyJhY2Nlc3MiOiB7InRva2VuIjogeyJpc3N1ZWRfYXQiOiAiMjAxNC0wNC0xMFQxMzo0MToyOS4yNTEzMzEiLCAiZXhwaXJlcyI6ICIyMDE0LTA0LTExVDEzOjQxOjI5WiIsICJpZCI6ICJwbGFjZWhvbGRlciIsICJ0ZW5hbnQiOiB7ImRlc2NyaXB0aW9uIjogIkFkbWluIFRlbmFudCIsICJlbmFibGVkIjogdHJ1ZSwgImlkIjogImM5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgIm5hbWUiOiAiYWRtaW4ifX0sICJzZXJ2aWNlQ2F0YWxvZyI6IFt7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzYvdjEvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgImlkIjogIjBmNTVlMWZjZmE0NDQ2MjNhMGNjZTRlNDMwZDJmZTNjIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogInZvbHVtZSIsICJuYW1lIjogImNpbmRlciJ9LCB7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjkyOTIiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIiwgImlkIjogImI2ODcxNjU3NmRhODQ2Njc4ZTg4NDg4NWExMmJiMTdhIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImltYWdlIiwgIm5hbWUiOiAiZ2xhbmNlIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3NC92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAiaWQiOiAiYzY5M2E2OGU5ODM0NGE4Yjg5NzY1MzFmYjhmMGE2MGIiLCAicHVibGljVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQifV0sICJlbmRwb2ludHNfbGlua3MiOiBbXSwgInR5cGUiOiAiY29tcHV0ZSIsICJuYW1lIjogIm5vdmEifSwgeyJlbmRwb2ludHMiOiBbeyJhZG1pblVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YyL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgInJlZ2lvbiI6ICJyZWdpb25PbmUiLCAiaW50ZXJuYWxVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJpZCI6ICIxYzU5ZjkwMGVhOTA0Nzc3ODEyNGM2NWYwODk1ZGFmZSIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCJ9XSwgImVuZHBvaW50c19saW5rcyI6IFtdLCAidHlwZSI6ICJ2b2x1bWV2MiIsICJuYW1lIjogImNpbmRlcnYyIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6MzUzNTcvdjIuMCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjUwMDAvdjIuMCIsICJpZCI6ICJiMzU2ZTYxYjU1OGI0ZWUzYTk2NTcyZjk3N2ExYzU0MCIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6NTAwMC92Mi4wIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImlkZW50aXR5IiwgIm5hbWUiOiAia2V5c3RvbmUifV0sICJ1c2VyIjogeyJ1c2VybmFtZSI6ICJhZG1pbiIsICJyb2xlc19saW5rcyI6IFtdLCAiaWQiOiAiY2JmZWQ0NDRkNWNjNDRhOTgxNWU4ZTAwODY5ZGMwMGEiLCAicm9sZXMiOiBbeyJuYW1lIjogImFkbWluIn1dLCAibmFtZSI6ICJhZG1pbiJ9LCAibWV0YWRhdGEiOiB7ImlzX2FkbWluIjogMCwgInJvbGVzIjogWyI2MGI1NDBhNGE4MjA0NThjODY0OThjNzI5YjJmMDMyNCJdfX19MYIBgTCCAX0CAQEwXDBXMQswCQYDVQQGEwJVUzEOMAwGA1UECAwFVW5zZXQxDjAMBgNVBAcMBVVuc2V0MQ4wDAYDVQQKDAVVbnNldDEYMBYGA1UEAwwPd3d3LmV4YW1wbGUuY29tAgEBMAcGBSsOAwIaMA0GCSqGSIb3DQEBAQUABIIBAJBS948FZkIzdg46mAf5Qly0z0fuXdCYPlACFNPxKzbGBGZHcy1UfuKhKmMUlVCS2HAx3UxEiGZPnI4KlqG+uIRQpzGy6HOLBEn2j+QOO76lfV-lYsbIBdlcRmfeMI8Lx+Z546UIeqNt8cmJWJNhKYnR45ydxt6L2nAqFPGuxPDuc5p04kaNg0RQ6kM2EAQWTrMAE0WPiaiNb0h4TM8N+mQHfl9fGctG09m9HG69os8mMFjddSB335WrPXSpHiHJHOJpKizEHsZ229poETtlVe4NGnvi6gGzGzPyQfGg+Lzq1tGMa6Wbiy2WVq2Z2matSLhVfn1lxJU+z7jQnGW18NE="
####################################################
Output is 
####################################################

HTTP/1.1 200 OK
Vary: X-Auth-Token
Content-Type: application/json
Content-Length: 1359
Date: Thu, 10 Apr 2014 13:53:39 GMT

{"endpoints": 
   [
       {"internalurl": "http://controller:8774/v2/%(tenant_id)s", "adminurl": "http://controller:8774/v2/%(tenant_id)s", "service_id": "96287ac914734ee5b93d66a43d01423b", "region": "regionOne", "id": "0833686a32024dc3ba7c62b75cb28d00", "publicurl": "http://controller:8774/v2/%(tenant_id)s"}, {"adminurl": "http://controller:8776/v1/%(tenant_id)s", "service_id": "43218d6888dd40e2bd45f9b3de6c764b", "region": "regionOne", "publicurl": "http://controller:8776/v1/%(tenant_id)s", "id": "64a0d3c06a284df29a5815a804af0aef", "internalurl": "http://controller:8776/v1/%(tenant_id)s"}, {"internalurl": "http://controller:8776/v2/%(tenant_id)s", "adminurl": "http://controller:8776/v2/%(tenant_id)s", "service_id": "c22e8cabdb1046f98e58864549a5d113", "region": "regionOne", "id": "9722cf7aee16488db8c8e47ef82ab8ac", "publicurl": "http://controller:8776/v2/%(tenant_id)s"}, {"internalurl": "http://controller:5000/v2.0", "adminurl": "http://controller:35357/v2.0", "service_id": "0505e7233deb4a1a8b414db0348527b8", "region": "regionOne", "id": "c0f4b30583254310b25ce8f4c9b8da25", "publicurl": "http://controller:5000/v2.0"}, {"adminurl": "http://controller:9292", "service_id": "6df4ba2a2c034737922a5a27553ff9fc", "region": "regionOne", "publicurl": "http://controller:9292", "id": "6e77e12545ba40df89976c46dad5cb28", "internalurl": "http://controller:9292"}]}




4.  To get the list of servers use this

curl -v -H "X-Auth-Token:MIIKDAYJKoZIhvcNAQcCoIIJ-TCCCfkCAQExCTAHBgUrDgMCGjCCCGIGCSqGSIb3DQEHAaCCCFMEgghPeyJhY2Nlc3MiOiB7InRva2VuIjogeyJpc3N1ZWRfYXQiOiAiMjAxNC0wNC0xMFQxMzo0MToyOS4yNTEzMzEiLCAiZXhwaXJlcyI6ICIyMDE0LTA0LTExVDEzOjQxOjI5WiIsICJpZCI6ICJwbGFjZWhvbGRlciIsICJ0ZW5hbnQiOiB7ImRlc2NyaXB0aW9uIjogIkFkbWluIFRlbmFudCIsICJlbmFibGVkIjogdHJ1ZSwgImlkIjogImM5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgIm5hbWUiOiAiYWRtaW4ifX0sICJzZXJ2aWNlQ2F0YWxvZyI6IFt7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzYvdjEvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgImlkIjogIjBmNTVlMWZjZmE0NDQ2MjNhMGNjZTRlNDMwZDJmZTNjIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YxL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogInZvbHVtZSIsICJuYW1lIjogImNpbmRlciJ9LCB7ImVuZHBvaW50cyI6IFt7ImFkbWluVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjkyOTIiLCAicmVnaW9uIjogInJlZ2lvbk9uZSIsICJpbnRlcm5hbFVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIiwgImlkIjogImI2ODcxNjU3NmRhODQ2Njc4ZTg4NDg4NWExMmJiMTdhIiwgInB1YmxpY1VSTCI6ICJodHRwOi8vY29udHJvbGxlcjo5MjkyIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImltYWdlIiwgIm5hbWUiOiAiZ2xhbmNlIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3NC92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQiLCAiaWQiOiAiYzY5M2E2OGU5ODM0NGE4Yjg5NzY1MzFmYjhmMGE2MGIiLCAicHVibGljVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjg3NzQvdjIvYzk4Nzk5NDg2YmJhNDEzOGE1YjVkMTcwODI3MzNlOGQifV0sICJlbmRwb2ludHNfbGlua3MiOiBbXSwgInR5cGUiOiAiY29tcHV0ZSIsICJuYW1lIjogIm5vdmEifSwgeyJlbmRwb2ludHMiOiBbeyJhZG1pblVSTCI6ICJodHRwOi8vY29udHJvbGxlcjo4Nzc2L3YyL2M5ODc5OTQ4NmJiYTQxMzhhNWI1ZDE3MDgyNzMzZThkIiwgInJlZ2lvbiI6ICJyZWdpb25PbmUiLCAiaW50ZXJuYWxVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCIsICJpZCI6ICIxYzU5ZjkwMGVhOTA0Nzc3ODEyNGM2NWYwODk1ZGFmZSIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6ODc3Ni92Mi9jOTg3OTk0ODZiYmE0MTM4YTViNWQxNzA4MjczM2U4ZCJ9XSwgImVuZHBvaW50c19saW5rcyI6IFtdLCAidHlwZSI6ICJ2b2x1bWV2MiIsICJuYW1lIjogImNpbmRlcnYyIn0sIHsiZW5kcG9pbnRzIjogW3siYWRtaW5VUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6MzUzNTcvdjIuMCIsICJyZWdpb24iOiAicmVnaW9uT25lIiwgImludGVybmFsVVJMIjogImh0dHA6Ly9jb250cm9sbGVyOjUwMDAvdjIuMCIsICJpZCI6ICJiMzU2ZTYxYjU1OGI0ZWUzYTk2NTcyZjk3N2ExYzU0MCIsICJwdWJsaWNVUkwiOiAiaHR0cDovL2NvbnRyb2xsZXI6NTAwMC92Mi4wIn1dLCAiZW5kcG9pbnRzX2xpbmtzIjogW10sICJ0eXBlIjogImlkZW50aXR5IiwgIm5hbWUiOiAia2V5c3RvbmUifV0sICJ1c2VyIjogeyJ1c2VybmFtZSI6ICJhZG1pbiIsICJyb2xlc19saW5rcyI6IFtdLCAiaWQiOiAiY2JmZWQ0NDRkNWNjNDRhOTgxNWU4ZTAwODY5ZGMwMGEiLCAicm9sZXMiOiBbeyJuYW1lIjogImFkbWluIn1dLCAibmFtZSI6ICJhZG1pbiJ9LCAibWV0YWRhdGEiOiB7ImlzX2FkbWluIjogMCwgInJvbGVzIjogWyI2MGI1NDBhNGE4MjA0NThjODY0OThjNzI5YjJmMDMyNCJdfX19MYIBgTCCAX0CAQEwXDBXMQswCQYDVQQGEwJVUzEOMAwGA1UECAwFVW5zZXQxDjAMBgNVBAcMBVVuc2V0MQ4wDAYDVQQKDAVVbnNldDEYMBYGA1UEAwwPd3d3LmV4YW1wbGUuY29tAgEBMAcGBSsOAwIaMA0GCSqGSIb3DQEBAQUABIIBAJBS948FZkIzdg46mAf5Qly0z0fuXdCYPlACFNPxKzbGBGZHcy1UfuKhKmMUlVCS2HAx3UxEiGZPnI4KlqG+uIRQpzGy6HOLBEn2j+QOO76lfV-lYsbIBdlcRmfeMI8Lx+Z546UIeqNt8cmJWJNhKYnR45ydxt6L2nAqFPGuxPDuc5p04kaNg0RQ6kM2EAQWTrMAE0WPiaiNb0h4TM8N+mQHfl9fGctG09m9HG69os8mMFjddSB335WrPXSpHiHJHOJpKizEHsZ229poETtlVe4NGnvi6gGzGzPyQfGg+Lzq1tGMa6Wbiy2WVq2Z2matSLhVfn1lxJU+z7jQnGW18NE=" http://controller:8774/v2/*c98799486bba4138a5b5d17082733e8d/servers  
#########################
output is 
#########################
> 
< HTTP/1.1 200 OK
< Content-Type: application/json
< Content-Length: 1040
< X-Compute-Request-Id: req-3bc9fc32-9aa3-4cf5-9d56-c4aa556a119e
< Date: Thu, 10 Apr 2014 13:57:59 GMT
< 
{"servers": [{"id": "e720c2ee-64c3-46d5-b115-f769880b3c8a", "links": [{"href": "http://controller:8774/v2/c98799486bba4138a5b5d17082733e8d/servers/e720c2ee-64c3-46d5-b115-f769880b3c8a", "rel": "self"}, {"href": "http://controller:8774/c98799486bba4138a5b5d17082733e8d/servers/e720c2ee-64c3-46d5-b115-f769880b3c8a", "rel": "bookmark"}], "name": "clogytest"}, {"id": "73e8218f-4b58-4df1-bb56-e2a7f956a82d", "links": [{"href": "http://controller:8774/v2/c98799486bba4138a5b5d17082733e8d/servers/73e8218f-4b58-4df1-bb56-e2a7f956a82d", "rel": "self"}, {"href": "http://controller:8774/c98799486bba4138a5b5d17082733e8d/servers/73e8218f-4b58-4df1-bb56-e2a7f956a82d", "rel": "bookmark"}], "name": "test"}, {"id": "d237f817-facc-4393-a2b7-9ef2c9bf24ab", "links": [{"href": "http://controller:8774/v2/c98799486bba4138a5b5d17082733e8d/servers/d237f817-facc-4393-a2b7-9ef2c9bf24ab", "rel": "self"}, {"href": "http://controller:8774/c98799486bba4138a5b5d17082733e8d/servers/d237f817-facc-4393-a2b7-9ef2c9bf24ab", "rel": "bookmark"}], "na* Connection #0 to host controller left intact
* Closing connection #0
me": "cirrOS"}]}
