Install and setup docker
==========================


Install Docker Driver
::
  git clone https://git.openstack.org/stackforge/nova-docker /opt/stack/nova-docker
  cd /opt/stack/nova-docker
  ./contrib/devstack/prepare_devstack.sh
  python setup.py install
  
Update the localrc file in devstack directory (Copy the fopllowing into local.conf in devstack directory and remove localrc file)

[local|localrc]]
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
# For Docker
VIRT_DRIVER=novadocker.virt.docker.DockerDriver
## Updating Default Services ##
disable_all_services

# core compute (glance / keystone / nova (+ nova-network))
ENABLED_SERVICES=g-api,g-reg,key,n-api,n-crt,n-obj,n-cpu,n-net,n-cond,n-sch,n-novnc,n-xvnc,n-cauth
# cinder
#ENABLED_SERVICES+=,c-sch,c-api,c-vol
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
CINDER_BRANCH=stable/kilo
GLANCE_BRANCH=stable/kilo
HORIZON_BRANCH=stable/kilo
KEYSTONE_BRANCH=stable/kilo
NOVA_BRANCH=stable/kilo
NEUTRON_BRANCH=stable/kilo

# Introduce glance to docker images
[[post-config|$GLANCE_API_CONF]]
[DEFAULT]
container_formats=ami,ari,aki,bare,ovf,ova,docker

# Configure nova to use the nova-docker driver
[[post-config|$NOVA_CONF]]
[DEFAULT]
compute_driver=novadocker.virt.docker.DockerDriver


Docker runtime configuration
::
  

Nova Compute Update
::

