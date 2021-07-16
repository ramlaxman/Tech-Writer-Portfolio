<!-----
NEW: Check the "Suppress top comment" option to remove this info from the output.

Conversion time: 0.341 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β30
* Fri Jul 16 2021 02:17:15 GMT-0700 (PDT)
* Source doc: Swift Configuration
* This is a partial selection. Check to make sure intra-doc links work.
----->

```
mount /dev/sda3
```
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
