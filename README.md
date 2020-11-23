Role Name
=========

A role to provision a machine with a user who has a secure password. Then create a csv file that can be imported into lastpass with all the user data.

Requirements
------------
- ansible < 2.8

Installation
------------
    ansible-galaxy install awol_linux.basesetup

Role Variables
--------------

- `my_pass:` the password that will be given to any user provisioned (default: random).  
- `username:` the username that will be provisioned (default: ansible-user).  
- `tmp_file:` set tmpfile name  (default /tmp/password{{ date and time }}. Please note using a existing file will cause errors.
- `sudo_group:` the group used for sudo authentication (default: wheel).  
- `create_ansible_user:` create ansible user and give him sudo no password (default: yes).

Dependencies
------------
- gantsign.ohmyzsh ansible role  
- https://galaxy.ansible.com/gantsign/oh-my-zsh

Example Playbook
----------------
    - hosts: all 
        become: true
        roles: 
            - role: basesetup

To set a default password for all the users you can set a password variable like so.

    - hosts: all 
      become: true
      roles: 
          - role: basesetup
            vars:
              - username: user1
              - my_pass: P@55w0rd

Would create a user named `user1` and set the `P@55w0rd`

If you would like to store your password securely you can use ansible-vault to create a encrypted field.
    
    [awol@ansible-server ~]$ ansible-vault encrypt_string P@55w0rd
    New Vault password: 
    Confirm New Vault password: 
    !vault |
          $ANSIBLE_VAULT;1.1;AES256
          61623239303164633131666339313436666565386530333630326135373834343634313863363964
          6136646263383231356235313833643837653731343537370a633634333864326437356161643334
          66393539356436616431353036646638643432396636616530366361653762373663366435383865
          6463663465343738360a613138376333663030666161393337386466313234663734323438386439
          3561
    Encryption successful
Then take the vault field and use it as a variable. 

    - hosts: all 
        become: true
        vars:
            ansible_user: root
        roles:
            - role: baseline-role
              vars:
                    username: awol 
                    my_pass: !vault |
                        $ANSIBLE_VAULT;1.1;AES256
                        61623239303164633131666339313436666565386530333630326135373834343634313863363964
                        6136646263383231356235313833643837653731343537370a633634333864326437356161643334
                        66393539356436616431353036646638643432396636616530366361653762373663366435383865
                        6463663465343738360a613138376333663030666161393337386466313234663734323438386439
                        3561

Then when you use the playbook make surr you use the flag.

    --ask-vault-pass

License
-------

GPLv2