Detach volume from non-existing instance
Context : A volume that is attached to an already deleted instanced
openstack volume set --state available <VOLUME>

cinder reset-state --state available --attach-status detached 211ea613-442e-42db-9438-e51fe2f46487

If the solution with the state doesn't work after some time, there are several ways to do that. But, the best way I've found was to do it directly from the DB. This solution is a litle bit tricky since it's required to modify 2 entries on the cinder and nova database and then delete the mapping for the volume attached on instance in nova DB.

Steps:

Go to a controller node. Access the MariaDB container. Access the Database.
Detach volume from cinder and Updated the volume status
    MariaDB [(none)]> use cinder;
    MariaDB [(cinder)]> update cinder.volumes set attach_status='detached',status='available'  where id='$volume_uuid';
Changed to nova DB
   MariaDB [(none)]> use nova;
Deleted the instance entry for that volume on the mapping table
   MariaDB [(nova)]> delete from block_device_mapping where not deleted and volume_id='$volume_uuid';
Finally, updated the nova bootindex on the mapping table for the volume root file system
   MariaDB [(nova)]> update nova.block_device_mapping  set boot_index=0 where not deleted and volume_id='$volume_uuid';
   
   
https://raymii.org/s/articles/Fix_inconsistent_Openstack_volumes_and_instances_from_Cinder_and_Nova_via_the_database.html
https://ask.openstack.org/en/question/66918/how-to-delete-volume-with-available-status-and-attached-to/?answer=66921#post-id-66921


openstack volume show 211ea613-442e-42db-9438-e51fe2f46487
nova volume-detach aa04d3e1-ffd7-48ee-af56-37942661598f 211ea613-442e-42db-9438-e51fe2f46487
