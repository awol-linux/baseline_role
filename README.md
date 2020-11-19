Role Name
=========

a role to provision a machine with a user who has a secure password. Then create a csv file that can be imported into lastpass with all the user data.

Requirements
------------
ansible < 2.8

Role Variables
--------------

- `my_pass:` the password that will be given to any user provisioned (default: random).  
- `username:` the username that will be provisioned.  
- `tmp_file:` set tmpfile name  (default /tmp/password{{ date and time }}. please note using a existing file will cause errors 
- `sudo_group:` the group used for sudo authentication (default: wheel)

Dependencies
------------
gantsign.ohmyzsh ansible role  
https://galaxy.ansible.com/gantsign/oh-my-zsh

Example Playbook
----------------
    - hosts: all 
      become: true
      roles: 
          - role: basesetup
            vars:
              - username: user1
              - my_pass: P@55w0rd
Would create a user named `user1` and set the `P@55w0rd`

License
-------

GPLv2