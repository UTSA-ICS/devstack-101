Implement ``nova listall``
--------------------------

This should mirror the functionality of ``nova list`` with the following additional capabilities:

* display list of deleted as well as active servers
* display the above for demo and for admin user


**Hint**

* first duplicate the ‘nova list’ functionality across the client and server and make sure ``nova listall`` does exactly what nova list is doing.
* Once this is working then start modifying the server method pertaining to listall to list all VMs (active and deleted)


**Debugging Hints are at https://github.com/UTSA-ICS/devstack-101/blob/master/Debugging%20hints.rst**
