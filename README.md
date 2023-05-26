Role Name
=========

Install and configure glusterfs servers and configure volumes. This can also setup TLS for the management channels. That includes generating TLS certs and CA for the servers in the cluster.

Requirements
------------

- geerlingguy.glusterfs

Role Variables
--------------

- gluster_repo_version: The glusterfs repo version to pass to `geerlingguy.glusterfs`. Defaults to `10`.
- gluster_force: If true set `force: yes` for `gluster.gluster.gluster_volume`. Defaults to `no`.
- gluster_cluster_group: The group of hosts in the cluster. Defaults to "all".
- gluster_mount_user (str): Default/global volume directory user. Defaults to `root`.
- gluster_mount_group (str): Default/global volume directory group. Defaults to `root`.
- gluster_mount_mode (str/octal): Default/global volume directory mode. Defaults to `0770`.
- gluster_volume_peers (list, optional): A list of peer hostnames. Defaults to the `inventory_hostname`s of hosts in the group given in `gluster_cluster_group`.
- gluster_volume_options (dict, optional): Default/global dict of glusterfs volume options. Defaults to an empty dict.
- gluster_volumes (list): A list of volumes to create.
  Options:
    - brick: The path of the brick for the volume.
    - mount_group (str, optional): Overrides `gluster_mount_group`. Defaults to `root`.
    - mount_mode (str/octal, optional): Overrides `gluster_mount_mode`. Defaults to `0770`.
    - mount_point (str): The path of the mount point of the volume. 
    - mount_user (str, optional): Overrides `gluster_mount_user`. Defaults to `root`.
    - name (str): Volume name.
    - options (dict): A dict of glusterfs volume options. This overrides `gluster_volume_options` for the volume. Defaults to an empty dict.
    - peers (list, optional): A list of peer hostnames. Overrides `gluster_volume_peers`. Defaults to the `inventory_hostname`s of hosts in the group given in `gluster_cluster_group`.
    - rebalance (bool, optional): See `gluster.gluster.gluster_volume` documentation. Defaults to `no`.
    - replicas (int/str, optional):  Defaults to `undefined`. when: item.replicas is defined and item.replicas != 'all'
- gluster_enable_tls_management (bool, optional): If true management TLS encryption is enabled. Defaults to `no`.

Dependencies
------------

- openssl: The `openssl` command is used if `gluster_enable_tls_management` is true.

Example Playbook
----------------

```
- name: Setup gluster cluster
  hosts: "production_swarm"
  become: yes
  roles:
    - role: haxwithaxe.gluster_cluster
      vars:
        gluster_repo_version: 10
        gluster_force: yes
        gluster_cluster_group: "production_swarm"
        gluster_volume_group: "docker"
        gluster_enable_tls_management: yes
        gluster_volumes:
          - name: swarm
            brick: /bricks/swarm
            mountpoint: /mnt/swarm
            options:
              server.ssl: !!str on
              client.ssl: !!str on
```

License
-------

GPLv3

Author Information
------------------

Created by (haxwithaxe)[https://github.com/haxwithaxe]

