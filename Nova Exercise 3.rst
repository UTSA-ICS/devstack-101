Policy Enforcement
------------------

**Part I**

* As “admin” user using the Horizon GUI or command line add a new role called ‘tadmin’ to the devstack installation
* Now associate this role with the ’demo’ user
* Update the policy for ‘nova’ such that when you type the command “nova usage-list” it allows the demo user to list usage data for all tenants
 - http://docs.openstack.org/admin-guide-cloud/content/keystone-concepts.html
 - http://docs.openstack.org/trunk/openstack-network/admin/content/ch_auth.html
 - nova policy is stored in /etc/nova/policy.json file.

**Part II**

* Update the policy for ‘tadmin’ to permit the execution of the following commands:
* Any keystone user management commands (create/update/delete users)
* Any keystone command to manage role (role assignment, update/ deletion)
* Add a custom policy check in Nova code that was added for exercise 2 to display deleted and active VMs ONLY for the ‘tadmin’ and ‘admin’ role and NOT for ‘demo’ role.
* The policy will need to be implemented in the policy.json file.

