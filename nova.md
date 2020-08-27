Flavor:\
```
openstack flavor create FLAVOR_NAME --id FLAVOR_ID \
    --ram RAM_IN_MB --disk ROOT_DISK_IN_GB --vcpus NUMBER_OF_VCPUS
```

--private : use if an individual user or group do it 

set flavor to a project : \
```
 openstack flavor set --project PROJECT_ID m1.extra_tiny
```
Show host usage statistics \
```
openstack host show [host]
```

Show instance usage statistics
```
nova diagnostics [server]
```

Get summary statistics for each project:
```
openstack usage list
```

