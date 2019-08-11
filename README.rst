==============================
 Ansible Role: nfsroot_images
==============================

This is an ansible role for setting up NFS root boot images that handles installing the filesystem, configuring it for readonly or read/write booting, and setting up the ansible user within each image. 

----------------
 Role Variables
----------------

Key role variables are documented with their default values below. See ``defaults/main.yml`` for a full list.

::

    nfsridef_addr: ""
    nfsridef_ansible_password: ""

These two variables must be defined as the IP address of the NFS server which will serve the prepared images, and a crypted password hash for the ansible user account.

::

    nfsroot_image_list: []

This is a list of dictionaries describing the nfsroot images to create. The ``path`` key is the only required key for each item. For all ``nfsridef_<variable>`` variables defined in the ``defaults``, the ``variable`` key can be set for a given dictionary to override that default value for that specific image.


------------------
 Example Playbook
------------------

::

    ---
    - hosts: localhost
      vars:
        nfsridef_addr: 10.0.0.1
        nfsridef_ansible_password: "{{ lookup('file', 'crypted_ansible_pw.txt') }}"
        nfsroot_image_list:
          - path: /data/nfsroot/cent7
            groupname: "Compute node"
            sshkey_types: ['rsa', 'ecdsa']
          
          - path: /data/nfsroot/cent7_rw
            readonly: False
      roles:
        - nfsroot_images
