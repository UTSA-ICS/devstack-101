Trace Nova client server code path
==================================

Run the following commands:

1. Log into your VM as stack user
2. Issue the following commands::

		cd devstack
		source openrc admin admin
		nova --debug list
3. Trace and document the code path that is taken from 'nova client' to 'nova server' for this list command to work. 
   The nova client code is located at ``/opt/stack/python-novaclient``
   and the nova server code is loctaed at ``/opt/stack/nova/nova``.
   
   * Check the client.py file in python-novaclient/novaclient/[nova version]/client.py
   * Check the shell.py file in python-novaclient/novaclient/[nova version]/shell.py
   * Find the method (function) that nova list calls


**Debugging Hints are at https://github.com/UTSA-ICS/devstack-101/blob/master/Debugging%20hints.rst**
