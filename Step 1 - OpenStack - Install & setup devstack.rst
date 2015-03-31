Install and setup devstack
==========================

Login to OpenStack Horizon portal (10.245.121.4)

Create a keypair
::
	Click on “Access & Security” Tab again and Click on the subTab “Key Pairs”
	Either create a new keypair or import an existing KeyPair.

Create an instance using the devstack-<release> snapshot.
::
	Click on “Instances” and then on “Launch Instance”
	Fill in the following fields:
      		- “Instance Name” : <Any meaningful name>
      		- “Flavor” : m1.medium	
      		- “Instance Boot Source” : Boot From Snapshot
      		- “Image Name” : devstack-juno
	Now click on “Launch”
	Click on the instance name and check the 'Log' to see when the VM login screen appears

Log in as stack to the server (Password is 'stack') and ensure that nova list works
::
	ssh stack@$server_ip 
	cd /opt/stack/devstack
	source openrc admin admin
	nova list

Ensure that there are no errors and this pases successfully. 
If not then please check out the "Issues" section for further debugging.
https://github.com/UTSA-ICS/devstack-101/issues
