Connect 2+ servers hosted on Hetzner using NFS and VLAN.

_Note 1: This comes with no support other than the instructions provided here._ 

_Note 2: This setup has been tested to work with standard Unionfs/Rclone VFS setup. Using either MergerFS or any non-standard setup will require you to tweak the appropriate mounts. You can look at the roles to see what changes need to be done._ 


# Install

In this example, we'll set our Feederbox as the NFS server and our Mediabox as the NFS client - this is so that the feeder data can be available to the media server.

There are 3 phases to the setup. They are broken down below. 

## Hetzner Robot

1. Log into [Hetzner Robot](https://robot.your-server.de/).

1. Create a VLAN (_vSwitch_) and add servers to it. Note the VLAN ID.

   [![](https://i.imgur.com/MOBrkTE.png)](https://i.imgur.com/MOBrkTE.png)

1. Setup Firewall.

   - Mediabox:

     [![](https://i.imgur.com/TzRhtmf.png)](https://i.imgur.com/TzRhtmf.png)

   - Feederbox:

     [![](https://i.imgur.com/PlJ0ays.png)](https://i.imgur.com/PlJ0ays.png)

## NFS Server (Feederbox)

1. Setup the Ansible role config.

   1. Add `vlan_id`. 

   1. `mount_client` setting is ignored for the NFS server (i.e. it will just use `2`).


      ```
      cd ~/community
      nano hetzner_nfs.yml
      ```

      ```yaml
      hetzner_nfs:
        vlan_id: 4001
        mount_client: 3
      ```

1. Run Ansible role to configure the NFS server.

   ```
   sudo ansible-playbook community.yml --tags hetzner_nfs_server
   ```

## NFS Client (Mediabox)


1. Setup the Ansible role config.

   1. Add `vlan_id`. 

   1. Add `mount_client`. 

      Note: `mount_client` will need to be either `3` or a number > `250`.

      ```
      cd ~/community
      nano hetzner_nfs.yml
      ```

      ```yaml
      hetzner_nfs:
        vlan_id: 4001
        mount_client: 3
      ```

1. Run Ansible role to configure the NFS client.

   ```
   sudo ansible-playbook community.yml --tags hetzner_nfs_client_mount
   ```


# Uninstall 

Simply run the following commands on their respective servers:

## NFS Server (Feederbox)

```
sudo ansible-playbook community.yml --tags hetzner_nfs_server_uninstall
```

## NFS Client (Mediabox)

```
sudo ansible-playbook community.yml --tags hetzner_nfs_client_unmount
```
