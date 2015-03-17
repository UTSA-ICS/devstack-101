Trace Nova client server code path
==================================

Run the following commands:

1. Log into your VM as stack user
2. Issue the following commands::

	cd devstack
	source openrc admin admin
	nova --debug list
3. Trace and document the code path that is taken from 'nova client' to 'nova server' for this list command to work. 
   The nova client code is located at ``/usr/local/lib/python2.7/dist-packages/novaclient``
   and the nova server code is loctaed at ``/opt/stack/nova/nova``.
