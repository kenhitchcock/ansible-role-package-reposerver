Role Name
=========

name: ansible-role-package-reposerver
The purpose of this role is to create a system that can serve packages to other systems for installation.

Requirements
------------

Registered to satellite or CDN, failing that, a ISO with packages will need to be mounted and a repo configured.


Role Variables
--------------

Most variables required for this role to run are currently set in the defaults directory of the role and dont need to be set. 


Example Playbook
----------------

- name: "Build Repo server" 
  hosts: reposerver  
  become: true

  tasks:
    - name: "Include role"
      include_role:
        name: ../roles/ansible-role-package-reposerver


License
-------

MIT

