apt-get install nova-novncproxy novnc nova-api nova-ajax-console-proxy nova-cert nova-conductor nova-consoleauth nova-doc nova-scheduler python-novaclient

CREATE DATABASE nova;
GRANT ALL PRIVILEGES ON nova.* TO 'nova'@'localhost' IDENTIFIED BY 'cloud123';
GRANT ALL PRIVILEGES ON nova.* TO 'nova'@'%' IDENTIFIED BY 'cloud123';
nova-manage db sync


my_ip=192.168.2.20
vncserver_listen=192.168.2.20
vncserver_proxyclient_address=192.168.2.20

keystone user-create --name=nova --pass=cloud123 --email=shripad@clearlogy.com
keystone user-role-add --user=nova --tenant=service --role=admin

keystone service-create --name=nova --type=compute --description="Nova Compute service"

keystone endpoint-create --service-id=96287ac914734ee5b93d66a43d01423b --publicurl=http://controller:8774/v2/%\(tenant_id\)s --internalurl=http://controller:8774/v2/%\(tenant_id\)s --adminurl=http://controller:8774/v2/%\(tenant_id\)s


