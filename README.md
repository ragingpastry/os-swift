Role Name
=========

Installs and configures OpenStack Swift Storage services.

Requirements
------------

This role has no external requirements other than Molecule for tests

Role Variables
--------------

exclude_drives
  * Array
  * This variable is a list which contains drives to exclude from Openstack Swift. These will usually be OS drives
    If you do not include a drive in this list then it **WILL** be formatted
  ```
  exclude_drives:
    - /dev/sda
    - /dev/sdb
  ```

mount_options
  * String
  * This variable contains a list of mount options to pass to the storage server for the swift drives.
  ```
  mount_options: noatime,nodiratime,nobarrier,logbufs=8
  ```

recon_directory

format_devices
  * Boolean
  * This variable controls the formatting of devices. By default this variable is set to False, meaning drives will 
    **NOT** be formatted. If the drives are not already formatted then the playbook will fail.

  * DO NOT SET THIS TO TRUE IF YOU ARE NOT PLANNING ON LOSING DATA

keystone_url
  * String
  * The hostname of the keystone server. This is usually 'controller'

swift_password
  * String
  * The pasword for the swift user in Keystone

keystone_admin_password
  * String
  * Admin password used to authenticate against keystone for account,service,endpoint creation

overwrite_ring_files
  * Boolean
  * If set to True this playbook will overwrite any ring files. This could be dangerous

swift_hash_path_suffix
  * String
  * Keep these values secret and do not change or lose them. 
  * Should be vault encrypted in production

swift_hash_path_prefix
  * String
  * Keep these values secret and do not change or lose them. 
  * Should be vault encrypted in production



Dependencies
------------

This role is dependent on Keystone being configured.

Example Playbook
----------------

    - hosts: swift-nodes
      roles:
         - role: os-swift-node
           exclude_drives:
             - /dev/sda
             - /dev/sdb
           format_devices: True
           keystone_admin_password: "{{ adminrcpassword }}"

License
-------

BSD

Author Information
------------------

Written by Nick Wilburn
