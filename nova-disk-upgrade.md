[root@rhel7 ~(keystone_admin)]# nova hypervisor-list
+----+---------------------+-------+---------+
| ID | Hypervisor hostname | State | Status  |
+----+---------------------+-------+---------+
| 1  | rhel7.0-packstack   | up    | enabled |
+----+---------------------+-------+---------+

[root@rhel7 ~(keystone_admin)]# nova hypervisor-show rhel7.0-packstack
(...)
| disk_available_least      | 57                                                                                                                                                                                                                                                                            |
| free_disk_gb              | 76 
                                     
[root@rhel7 ~(keystone_admin)]# nova service-list
nova service+----+------------------+-------------------+----------+---------+-------+----------------------------+-----------------+
| Id | Binary           | Host              | Zone     | Status  | State | Updated_at                 | Disabled Reason |
+----+------------------+-------------------+----------+---------+-------+----------------------------+-----------------+
| 1  | nova-consoleauth | rhel7.0-packstack | internal | enabled | up    | 2016-03-01T21:47:21.000000 | -               |
| 2  | nova-scheduler   | rhel7.0-packstack | internal | enabled | up    | 2016-03-01T21:47:12.000000 | -               |
| 3  | nova-conductor   | rhel7.0-packstack | internal | enabled | up    | 2016-03-01T21:47:20.000000 | -               |
| 6  | nova-compute     | rhel7.0-packstack | nova     | enabled | up    | 2016-03-01T21:47:18.000000 | -               |
| 7  | nova-cert        | rhel7.0-packstack | internal | enabled | up    | 2016-03-01T21:47:21.000000 | -               |
+----+------------------+-------------------+----------+---------+-------+----------------------------+-----------------+
(...)

[root@rhel7 ~(keystone_admin)]# nova service-disable rhel7.0-packstack nova-compute
+-------------------+--------------+----------+
| Host              | Binary       | Status   |
+-------------------+--------------+----------+
| rhel7.0-packstack | nova-compute | disabled |
+-------------------+--------------+----------+

[root@rhel7 ~(keystone_admin)]# mkfs.ext4 /dev/vdb

[root@rhel7 ~(keystone_admin)]# mv /var/lib/nova/instances/ /var/lib/nova/instances2

[root@rhel7 ~(keystone_admin)]# mkdir /var/lib/nova/instances

[root@rhel7 ~(keystone_admin)]# echo "/dev/vdb  /var/lib/nova/instances ext4  defaults 0 0" >> /etc/fstab 

[root@rhel7 ~(keystone_admin)]# mount /var/lib/nova/instances

[root@rhel7 ~(keystone_admin)]# cp -a /var/lib/nova/instances2/* /var/lib/nova/instances

[root@rhel7 ~(keystone_admin)]# restorecon -R /var/lib/nova/instances

[root@rhel7 ~(keystone_admin)]# chown nova. /var/lib/nova/instances -R

[root@rhel7 ~(keystone_admin)]# nova service-enable rhel7.0-packstack nova-compute
+-------------------+--------------+---------+
| Host              | Binary       | Status  |
+-------------------+--------------+---------+
| rhel7.0-packstack | nova-compute | enabled |
+-------------------+--------------+---------+

[root@rhel7 ~(keystone_admin)]# nova hypervisor-show rhel7.0-packstack
(...)
| disk_available_least      | 92                                                                                                                                                                                                                                                                            |
| free_disk_gb              | 95                                                                                                                                                                                                                                                                            |
(...)




