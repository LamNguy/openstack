
Create subnetwork 

```
openstack subnet create --network provider \
  --allocation-pool start=START_IP_ADDRESS,end=END_IP_ADDRESS \
  --dns-nameserver DNS_RESOLVER --gateway PROVIDER_NETWORK_GATEWAY \
  --subnet-range PROVIDER_NETWORK_CIDR provider
```

example : 

```
openstack subnet create --network provider \
  --allocation-pool start=10.10.1.151,end=10.10.1.159 \
  --dns-nameserver 8.8.8.8 --gateway 10.10.0.1 \
  --subnet-range 10.10.0.0/23 provider
```
