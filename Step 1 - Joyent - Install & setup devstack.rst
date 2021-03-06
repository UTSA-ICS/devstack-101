Install and setup devstack
==========================

Log in as root to the server
::
	ssh root@$server_ip 
	
Now add an entry for your hostname to the /etc/hosts file.
::
	echo "VM_IP_ADDRESS   $HOSTNAME"  >> /etc/hosts
	[e.g.-> echo "10.245.122.27 $HOSTNAME" >> /etc/hosts]
	
Create the 'stack' user and update it in the sudoers file
::
	adduser stack
	echo "stack ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

Install git and exit the server
::
	apt-get install -qqy git
	exit

Now Log in as 'stack' user and download devstack code
::
	ssh stack@$server_ip
	git clone -b stable/icehouse https://github.com/openstack-dev/devstack.git

Create the localrc file and then run the startup script for devstack
::
	cd devstack
	cat >> localrc <<EOF
	DEST=/opt/stack
	ADMIN_PASSWORD=admin
	MYSQL_PASSWORD=admin
	RABBIT_PASSWORD=admin
	SERVICE_TOKEN=admin
	SERVICE_PASSWORD=admin
	LOGFILE=/opt/stack/logs/stack.log
	SCREEN_LOGDIR=/opt/stack/logs
	VERBOSE=True
	## Controller Host ##
	# HOST_IP=<IP ADDRESS>
	# MULTI_HOST=1
	## Network nova-network ##
	FLAT_INTERFACE=eth0
	FIXED_RANGE=172.24.17.0/24
 	FIXED_NETWORK_SIZE=254
 	FLOATING_RANGE=192.168.1.128/25
	## Updating Default Services ##
	disable_all_services

	# core compute (glance / keystone / nova (+ nova-network))
	ENABLED_SERVICES=g-api,g-reg,key,n-api,n-crt,n-obj,n-cpu,n-net,n-cond,n-sch,n-novnc,n-xvnc,n-cauth
	# cinder
	ENABLED_SERVICES+=,c-sch,c-api,c-vol
	# heat
	#ENABLED_SERVICES+=,h-eng,h-api,h-api-cfn,h-api-cw
	# dashboard
	ENABLED_SERVICES+=,horizon
	# additional services
	ENABLED_SERVICES+=,rabbit,tempest,mysql
	# To enable Neutron
	#DISABLE_SERVICES=n-net
	#ENABLED_SERVICES+=,q-svc,q-agt,q-dhcp,q-l3,q-meta
	# Swift Services
	#ENABLED_SERVICES+=,s-proxy,s-object,s-container,s-account
	#SWIFT_HASH=66a3d6b56c1f479c8b4e70ab5c2000f5
	#SWIFT_REPLICAS=1
	#SWIFT_DATA_DIR=/opt/stack/data
	#
	## Logs ##
	SCREEN_LOGDIR=/opt/stack/logs/screen
	KEYSTONE_TOKEN_FORMAT=PKI
	####################
	# Branch specifics
	####################
	CINDER_BRANCH=stable/icehouse
	GLANCE_BRANCH=stable/icehouse
	HORIZON_BRANCH=stable/icehouse
	KEYSTONE_BRANCH=stable/icehouse
	NOVA_BRANCH=stable/icehouse
	NEUTRON_BRANCH=stable/icehouse
	EOF

	./stack.sh

Ensure that there are no errors and this pases successfully. 
If not then please check out the "Issues" section for further debugging.
https://github.com/UTSA-ICS/devstack-101/issues
