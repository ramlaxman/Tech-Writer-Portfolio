mount /dev/sda3
swift stat
gedit /etc/fstab
mkdir -p /srv/node/sda3
mount /srv/node/sda3
chown -R swift:swift /srv/node
keystone endpoint-delete e04abd33fc374f4abbe2afbca5d8dd12
keystone endpoint-list
keystone service-list
keystone endpoint-create --service-id=cbbaae18e016455d8854e9d8aa2c18ce --publicurl='http://computenode:8080/v1/AUTH_%(tenant_id)s' --internalurl='http://computenode:8080/v1/AUTH_%(tenant_id)s' --adminurl=http://computenode:8080
swift-init all restart
service memcached restart
swift stat
swift-init all start
sudo bash
source openrc.sh
swift stat
sudo bash
source openrc.sh
swift stat
sudo bash
source openrc.sh
swift stat
touch test.txt
gedit test.txt
touch test2.txt
gedit test2.txt
swift upload myfiles test.txt
swift upload myfiles test2.txt
swift download myfiles
cd /home/computenc/ && mkdir sample
cd sample/
swift download myfiles
gedit test
gedit test.txt
gedit test2.txt
swift stat
