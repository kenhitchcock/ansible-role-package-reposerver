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
|reporoot| Path to the where repos will be exposed via httpd | yes |"/var/www/html/repos"|
|repofilename|Directory name of where all repos will be stored.|yes|"custom_repos"|
|repogpgcheck|Used to mark repos to either use or done use gpgchecks|yes|"no"|
|unregisterreposvr|Will be used to unregister repo server from cdn or satellite|yes|"yes"|
|PACKAGES|Dictionary of packages that will be installed by the role.|Yes|httpd,createrepo,firewalld,zip,unzip|
|FIREWALL_SERVICES|Firewall services to open in the firewall, NOT ports for now.|yes|http,https,ssh|
|REPOS| Dictionary of repos to build and provide, example below | yes | |
|reposvr_filetype|accepts archive, iso for now|yes||
|reposvr_syncmeth|Used to determine how files will be transfered to system, accepted options are 'web','file' and 'sync'|yes||

### Example dictionary of RPM repos to build
```
  REPOS:
    RHEL7RPMS:
      reposvr_filename: "rhel77.zip"
      reposvr_filetype: "archive"
      reposvr_webloc: "http://192.168.122.1/rhel77/"
      reposvr_fileloc: "files/"
      reposvr_syncmeth: "web"
      reposvr_repodir: "rhel7"
      reposvr_reponame: "rhel7"
    CDNRHEL7HARPMS:
      reposvr_filename: "rhel-ha-for-rhel-7-server-rpms"
      reposvr_filetype: ""
      reposvr_extracteddir: ""
      reposvr_webloc: ""
      reposvr_fileloc: ""
      reposvr_syncmeth: "sync"
      reposvr_repodir: "rhel7-ha"
      reposvr_reponame: "rhel7-ha-for-rhel7-server-rpms"
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

