==============================
 Ansible Role: nfsroot_images
==============================

This is an ansible role for setting up NFS root boot images that handles installing the filesystem, configuring it for readonly or read/write booting, and setting up the ansible user within each image. 

----------------
 Role Variables
----------------

Key role variables are documented with their default values below. See ``defaults/main.yml`` for a full list.

::

    nfsroot_image_list: []

This is a list of dictionaries describing the nfsroot images to create. Each 
dictionary should define the following keys: ``path`` is the path on the 
filesystem to install the image into, ``addr`` is the NFS server's IP address 
that the boot images will mount, ``groupname`` is the yum install group to use, 
``releasever`` should be the version to install, ``sshkey_types`` is a list of 
SSH key type pairs to generate, and ``readonly`` is a boolean for whether the 
image should be prepared as readonly or readwrite.

------------------
 Example Playbook
------------------

::

    ---
    - hosts: localhost
      vars:
        nfsroot_image_list:
          - path: /data/nfsroot/cent7
            addr: 10.0.0.1
            groupname: "Minimal install"
            releasever: 7
            sshkey_types: ['rsa', 'ecdsa']
            readonly: False
      roles:
        - nfsroot_images
