package-reposerver
=========

name: ansible-role-package-reposerver
The purpose of this role is to create a system that can serve packages to other systems for installation.

Requirements
------------

Registered to satellite or CDN, failing that, a ISO with packages will need to be mounted and a repo configured.

Role Variables
--------------
Most variables required for this role to run are currently set in the defaults directory of the 
role and dont need to be set. 

| Variable | Description | Required | Defaults |
|:---------|:------------|:---------|:---------|
|reporoot| Path to the where repos will be exposed via httpd | yes | "/var/www/html/repos"|
|REPOS| Dictionary of repos to build and provide, example below | yes | |
|reposvr_filetype|accepts archive, iso for now|yes||
|reposvr_useweb|Used to determine how files will be transfered to system|yes||

```
  REPOS:
    RHEL7RPMS:
      reposvr_filename: "rhel77.zip"
      reposvr_filetype: "archive"
      reposvr_webloc: "http://192.168.122.1/rhel77/OS"
      reposvr_fileloc: "files/"
      reposvr_useweb: "yes"
      reposvr_repodir: "rhel7"
      reposvr_reponame: "rhel7"
```
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

