1. Edited the    /etc/sysconfig/libvirtd and changed LIBVIRTD_ARGS="--listen"
2. /etc/libvirt/libvirtd.conf
listen_tls = 0
listen_tcp = 1
3. restarted libvirtd to make sure it is listening on 16509
4. Also had to edit iptables to accept 16509
