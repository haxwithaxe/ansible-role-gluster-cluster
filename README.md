Role Name
=========

Install glusterfs and configure a volume.

Requirements
------------


Role Variables
--------------

gluster_repo_version: 10
gluster_brick: "/bricks/brick1"
gluster_force: "no"
gluster_cluster_group: "all"
gluster_mount_point: "/mnt/brick1"
gluster_name: "brick1"
gluster_volume_user: "root"
gluster_volume_group: "root"
gluster_volume_mode: "0770"

Dependencies
------------

geerlingguy.glusterfs

Example Playbook
----------------

```
- name: Setup gluster cluster
  hosts: "production_swarm"
  become: yes
  vars:
    gluster_repo_version: 10
    gluster_name: "docker-volumes"
    gluster_brick: "/bricks/docker-volumes"
    gluster_mount_point: "/mnt/docker-volumes"
    gluster_force: yes
    gluster_cluster_group: "production_swarm"
    gluster_volume_group: "docker"
  roles:
    - "haxwithaxe.gluster_cluster"
```

License
-------

GPLv3

Author Information
------------------

Created by (haxwithaxe)[https://github.com/haxwithaxe]
