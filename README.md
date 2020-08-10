# openstack
**User Management**
Create user alice

`
 openstack user create --password-prompt --email alice@example.com alice
`

Create a project named acme:

`
openstack project create acme --domain default
`

Create a domain named emea:

 openstack --os-identity-api-version=3 domain create emea
 
 
 Create a role named compute-user:
 `
  openstack role create compute-user
  `
  
  The Identity service assigns a project and a role to a user. You might assign the compute-user role to the alice user in the acme project:
  
  openstack role add --project acme --user alice compute-user

Assign a role¶
To assign a user to a project, you must assign the role to a user-project pair.

Assign a role to a user-project pair:

$ openstack role add --user USER_NAME --project PROJECT_NAME ROLE_NAME
For example, assign the new-role role to the demo user and test-project project pair:

$ openstack role add --user demo --project test-project new-role
Verify the role assignment:

$ openstack role assignment list --user USER_NAME \
  --project PROJECT_NAME --names
+-------------+--------------+-------+--------------+--------+--------+-----------+
| Role        | User         | Group | Project      | Domain | System | Inherited |
+-------------+--------------+-------+--------------+--------+--------+-----------+
| new-role    | demo@Default |       | demo@Default |        |        | False     |
| member      | demo@Default |       | demo@Default |        |        | False     |
| anotherrole | demo@Default |       | demo@Default |        |        | False     |
+-------------+--------------+-------+--------------+--------+--------+-----------+


