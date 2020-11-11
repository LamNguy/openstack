To select the host where instances are launched, use the --availability-zone ZONE:HOST:NODE parameter on the openstack server create command. \
```
$ openstack server create --image IMAGE --flavor m1.tiny \
  --key-name KEY --availability-zone ZONE:HOST:NODE \
  --nic net-id=UUID SERVER
 ```
 
 HOST and NODE are optional parameters. In such cases, use the --availability-zone ZONE::NODE, --availability-zone ZONE:HOST or --availability-zone ZONE.
 
 
 To specify which roles can launch an instance on a specified host, enable the create:forced_host option in the policy.json file. By default, this option is enabled for only the admin role. If you see Forbidden (HTTP 403) in return, then you are not using admin credentials.\
 
 openstack availability zone list \
 openstack host list \
 openstack hypervisor list
