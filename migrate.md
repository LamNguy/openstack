1. Edited the    /etc/sysconfig/libvirtd and changed LIBVIRTD_ARGS="--listen"\
2. /etc/libvirt/libvirtd.conf\
```
listen_tls = 0
listen_tcp = 1
listen_addr = "0.0.0.0"
tcp_port= 16509
```
3. restarted libvirtd to make sure it is listening on 16509\
4. Also had to edit iptables to accept 16509\

Edit \
Libvirt options allows cloud administrator to configure related\
libvirt hypervisor driver to be used within an OpenStack deployment.https://docs.openstack.org/nova/pike/admin/ssh-configuration.html \
Almost all of the libvirt config options are influence by ``virt_type`` config which describes the virtualization type (or so called domain type) libvirt should use for specific features such as live migration, snapshot.\
vi /etc/nova/nova.conf
```
[libvirt]
virt_type = qemu
live_migration_uri = qemu+tcp://%s/system
```



Migrate instances: move an instance from one host to another 

openstack server migrate --live TARGET_HOST VM_INSTANCE


To migrate an instance and watch the status, use this example script:

```
#!/bin/bash

# Provide usage
usage() {
echo "Usage: $0 VM_ID"
exit 1
}

[[ $# -eq 0 ]] && usage

# Migrate the VM to an alternate hypervisor
echo -n "Migrating instance to alternate host"
VM_ID=$1
openstack server migrate $VM_ID
VM_OUTPUT=$(openstack server show $VM_ID)
VM_STATUS=$(echo "$VM_OUTPUT" | grep status | awk '{print $4}')
while [[ "$VM_STATUS" != "VERIFY_RESIZE" ]]; do
echo -n "."
sleep 2
VM_OUTPUT=$(openstack server show $VM_ID)
VM_STATUS=$(echo "$VM_OUTPUT" | grep status | awk '{print $4}')
done
nova resize-confirm $VM_ID
echo " instance migrated and resized."
echo;

# Show the details for the VM
echo "Updated instance details:"
openstack server show $VM_ID

# Pause to allow users to examine VM details
read -p "Pausing, press <enter> to exit."
```
***Configure ssh between two compute node***
[link](https://docs.openstack.org/nova/pike/admin/ssh-configuration.html)

Configure ssh between two host

https://docs.openstack.org/nova/queens/admin/ssh-configuration.html#cli-os-migrate-cfg-ssh
