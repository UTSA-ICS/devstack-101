Trace Nova client server code path
==================================

Run the following commands:

1. Log into your VM as stack user;
2. Issue the following commands::

		cd devstack
	 	source openrc admin admin
	 	nova --debug list
3. Trace and document the code path that is taken from 'nova client' to 'nova server' for this list command to work

		The nova client code is at the following directory:
			``/usr/local/lib/python2.7/dist-packages/novaclient``
	
		The nova server code is at the following directory:
			``/opt/stack/nova/nova``


Proposed Change
===============

Basically, three main changes are proposed:

1. Propagate provided filters from controller to manager and driver levels;
2. Make the backend drivers consider filtering when executing list role
   assignment queries;
3. Move the code of expansion of inherited and group role assignments from the
   controller to the manager level.
