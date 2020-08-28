For keystone to observe implied roles, the infer_roles setting must be enabled in /etc/keystone/keystone.conf:

```
[token]
infer_roles = true
```

You can prevent certain roles from being implied onto a user. For example, in /etc/keystone/keystone.conf, you can add a ListOpt of roles:

```
[assignment]
prohibited_implied_role = admin
```
This will prevent a user from ever being assigned a role implicitly. Instead, the user will need to be explicitly granted access to that role.

Create role that implies on domain 

```
openstack role create operators --role-domain domain-corp01
```

Grant [group] permission to access [project] using [role]

```
 openstack role add _member_ --group grp-Auditors --project demo
 ```
 
 4.1.3. Set Object Storage Quotas for a User
Object Storage quotas can be classified under the following categories:

Container quotas - Limits the total size (in bytes) or number of objects that can be stored in a single container.
Account quotas - Limits the total size (in bytes) that a user has available in the Object Storage service.


5.2.1.1. Create the Project and Subprojects
You can implement Hierarchical Multitenancy (HMT) using keystone domains and projects. Begin by creating a new domain and then creating a project within that domain. You can then add subprojects to that project. You can also promote a user to administrator of a subproject by adding the user to the admin role for that subproject.


.2.1.2. Granting Access to Users
By default, a newly-created project has no assigned roles. When you assign role permissions to the parent project, you can include the --inherited flag to instruct the subprojects to inherit the assigned permissions from the parent project. For example, a user with admin role access to the parent project will also have admin access to the subprojects.










 
