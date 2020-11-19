Role Name
=========

a role to provision a machine with a user who has a secure password. Then create a csv file that can be imported into lastpass with all the user data.

Requirements
------------
ansible < 2.8

Role Variables
--------------

my_pass: the password that will be given to any user provisioned (default: random).  
username: the username that will be provisioned.  
'working on this but' tmpfile: set tmpfile name  (default /tmp/password {{ based on date and time }}.  
sudo_group: the group used for sudo authentication (default: wheel)

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
License
-------

GPLv2