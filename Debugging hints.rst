URL Routing
-----------

For routing of URL to method name look at this file on nova server:
``/opt/stack/nova/nova/api/openstack/compute/__init__.py``

To understand how this works read these 2 links:	
http://docs.openstack.org/developer/nova/devref/addmethod.openstackapi.html#routing
http://docs.openstack.org/developer/nova/devref/addmethod.openstackapi.html#controllers-and-actions

This is a the doc for the routes module that is used to implement the URL routing in openstack. Read this thoroughly!
https://routes.readthedocs.org/en/latest/introduction.html
https://routes.readthedocs.org/en/latest/glossary.html

Traceback
---------
Add traceback to the code and check the stack trace to see code path:
# Add the following line to the import section of a python file you are looking at
import traceback
# Add the following line to the any location where you want the stack to be printed
traceback.print_stack()

	
Documentation links
-------------------

http://docs.openstack.org/developer/nova/devref/index.html
https://github.com/openstack/nova
http://docs.openstack.org/trunk/openstack-compute/admin/content/
http://docs.openstack.org/api/openstack-compute/2/content/

File/content search tips
-------------------------

To search for a file ‘foo’ under the current directory (recursive search)
	find . |grep foo
To search for a keyword ‘bar’ (case insensitive “-i”) under the current directory (recursive search “-r”), 
	grep -i -r bar *
	grep -i -r bar * |grep -v tests ---> (“-v” says exclude this from my search) 

Run nova api such that it is logged to nova_api.log file
---------------------------------------------------------
::

	screen -r stack
	Ctrl+a+n	-> Use the control command (a+n) to go to ‘n-api’ (Nova API)
	Ctrl+C 		-> to stop Nova API process
	cd /opt/stack/nova && /opt/stack/nova/bin/nova-api > /tmp/nova_api.log 2>&1
	Logs are now being written to /tmp/nova_api.log file.
	Ctrl+a+d	-> to exit out of screen
	you can now run ‘less’ on the log file to search through it. 
	less /tmp/nova_api.log
	Ctrl+F		-> in ‘less’ to update the file with live data
	Ctrl+C		-> to cancel and go back to search mode in ‘less’
 
     
