GRANT ALL PRIVILEGES ON glance.* TO 'glance'@'localhost' IDENTIFIED BY 'cloud123';

GRANT ALL PRIVILEGES ON glance.* TO 'glance'@'%' IDENTIFIED BY 'cloud123';

source openrc.sh

keystone user-create --name=glance --pass=cloud123 --email=shripad@clearlogy.com --os-auth-url=http://controller:35357/v2.0

keystone user-role-add --user=glance --tenant=service --role=admin

### following command generates the service ID ##########

keystone service-create --name=glance --type=image --description="Glance Image Service"

keystone endpoint-create --service-id=6df4ba2a2c034737922a5a27553ff9fc --publicurl=http://controller:9292 --internalurl=http://controller:9292 --adminurl=http://controller:9292

####glance image-create --name=imageLabel --disk-format=fileFormat --container-format=containerFormat --is-public=accessValue < imageFile

glance image-create --name="CirrOS 0.3.1" --disk-format=qcow2 --container-format=bare --is-public=true < cirros-0.3.1-x86_64-disk.img

glance image-list

