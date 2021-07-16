GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' IDENTIFIED BY 'cloud123';
GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'%' IDENTIFIED BY 'cloud123';

export OS_SERVICE_TOKEN=5bdc7674848d94bf499b
export OS_SERVICE_ENDPOINT=http://controller:35357/v2.0

keystone tenant-create --name=admin --description="Admin Tenant"
keystone tenant-create --name=service --description="Service Tenant"

keystone user-create --name=admin --pass=cloud123 --email=shripad@clearlogy.com

keystone role-create --name=admin

keystone user-role-add --user=admin --tenant=admin --role=admin

keystone service-create --name=keystone --type=identity --description="Keystone Identity Service"

keystone endpoint-create --service-id=0505e7233deb4a1a8b414db0348527b8 --publicurl=http://controller:5000/v2.0 --internalurl=http://controller:5000/v2.0 --adminurl=http://controller:35357/v2.0

unset OS_SERVICE_TOKEN OS_SERVICE_ENDPOINT

keystone --os-username=admin --os-password=cloud123 --os-auth-url=http://controller:35357/v2.0 token-get

keystone --os-username=admin --os-password=cloud123 --os-tenant-name=admin --os-auth-url=http://controller:35357/v2.0 token-get

