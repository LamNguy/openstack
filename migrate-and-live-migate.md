1. Edited the    /etc/sysconfig/libvirtd and changed LIBVIRTD_ARGS="--listen"
2. /etc/libvirt/libvirtd.conf
listen_tls = 0
listen_tcp = 1
listen_addr = "0.0.0.0"
tcp_port= 16509
3. restarted libvirtd to make sure it is listening on 16509
4. Also had to edit iptables to accept 16509


vi /etc/nova/nova.conf

[libvirt]
#
# Libvirt options allows cloud administrator to configure related
# libvirt hypervisor driver to be used within an OpenStack deployment.https://docs.openstack.org/nova/pike/admin/ssh-configuration.html
#
# Almost all of the libvirt config options are influence by ``virt_type`` config
# which describes the virtualization type (or so called domain type) libvirt
# should use for specific features such as live migration, snapshot.

virt_type = qemu
live_migration_uri = qemu+tcp://%s/system


***Configure ssh between two compute node***
[link](https://docs.openstack.org/nova/pike/admin/ssh-configuration.html)
