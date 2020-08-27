# openstack
**Block Storage**

Create a volume : \
`$ openstack volume create --size volume_size [volume_name]` 

Attatch volume to an instance : \
`$ openstack server add volume INSTANCE_NAME VOLUME_NAME` 

Increase block storage api throughput : \ 

/etc/cinder/cinder.conf --> osapi_volume_workers [ NUM_CORES ] \
or \
```
openstack-config --set /etc/cinder/cinder.conf \
  DEFAULT osapi_volume_workers CORES
```
***Create an instance from a volume*** \
Create volume from image :  \ 
```
$ openstack volume create --image IMAGE_ID --size SIZE_IN_GB bootable_volume
```
Create instance from volume : \
```
 openstack server create --flavor c1.r0.v1 \
 --nic net-id=8cef69d5-9cf6-4d24-b88b-072f2d6273ce \
 --volume 5c07146b-f2ed-4702-ac81-dbe86064affb \
 --key-name my-key-2 \
 --security-group 320b3e1d-07e3-4ee5-80e6-2506e1f3ae2c \
 --block-device-mapping sdb=f3c900d7-af0b-4860-be74-802915bcab9f:::true \
 cirros_insance
```
--block-device-mapping 
```
nova boot --flavor c1.r0.v1 --nic net-id=8cef69d5-9cf6-4d24-b88b-072f2d6273ce \
--block-device source=volume,id=9dc3f63c-865d-4dab-8ccc-6e3a06be93cf,dest=volume,size=1,shutdown=preserve,bootindex=0 \
--key-name my-key-2 \
--security-groups 320b3e1d-07e3-4ee5-80e6-2506e1f3ae2c \
cirros_vol
```

[link](https://docs.openstack.org/nova/latest/user/launch-instance-from-volume.html#create-volume-from-image-and-boot-instance)


***Migrate volume*** \
```
cinder get-pools
cinder-manage host list
cinder manageable-list [host]os-storage@lvm
cinder-manage service list

```




More option : \
`openstack volume create --help` \
https://docs.openstack.org/python-openstackclient/pike/cli/command-objects/volume.html#top

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

#### Create virtual network

**For provider network** : 

![](https://docs.openstack.org/install-guide/_images/network1-connectivity.png)

Creat the provider network : \
`$ openstack network create  --share --external \
  --provider-physical-network provider \
  --provider-network-type flat provider`
  
MAC: media acccess control /
Ethernet network : Layer 2 or L2 /

**Launch an instance ** 


