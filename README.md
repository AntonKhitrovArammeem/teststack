# teststack

The test task for the SRE engineer candidates

-All the files are encrypted with ansible-vault

-Test stack includes django-sample-app and postgres 9.6, just run 'ansible-playbook django.yml -i testhost --ask-vault-pass' .You will be prompted for ansible-vault password for encrypted files 

-No additional Ansible modules required to be installed, tested with Ansible 2.7.10

-As the result you should receive the following output log:


root@instance-1:/etc/ansible# ansible-playbook django.yml -i testhost --ask-vault-pass
Vault password:
[DEPRECATION WARNING]: Instead of sudo/sudo_user, use become/become_user and make sure become_method is 'sudo' (default). This feature will be removed in
version 2.9. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.

PLAY [all] **************************************************************************************************************************************************

TASK [Gathering Facts] **************************************************************************************************************************************
ok: [10.156.0.2]

TASK [copy] *************************************************************************************************************************************************
ok: [10.156.0.2]

TASK [copy] *************************************************************************************************************************************************
changed: [10.156.0.2]

TASK [copy] *************************************************************************************************************************************************
ok: [10.156.0.2]

TASK [copy] *************************************************************************************************************************************************
ok: [10.156.0.2]

TASK [copy] *************************************************************************************************************************************************
ok: [10.156.0.2]

TASK [shell] ************************************************************************************************************************************************
 [WARNING]: Consider using the replace, lineinfile or template module rather than running 'sed'.  If you need to use command because replace, lineinfile or
template is insufficient you can add 'warn: false' to this command task or set 'command_warnings=False' in ansible.cfg to get rid of this message.

changed: [10.156.0.2]

TASK [shell] ************************************************************************************************************************************************
 [WARNING]: Consider using the apt module rather than running 'apt-get'.  If you need to use command because apt is insufficient you can add 'warn: false'
to this command task or set 'command_warnings=False' in ansible.cfg to get rid of this message.

changed: [10.156.0.2]

TASK [shell] ************************************************************************************************************************************************
 [WARNING]: Consider using the file module with state=directory rather than running 'mkdir'.  If you need to use command because file is insufficient you
can add 'warn: false' to this command task or set 'command_warnings=False' in ansible.cfg to get rid of this message.

changed: [10.156.0.2]

TASK [shell] ************************************************************************************************************************************************
changed: [10.156.0.2]

TASK [shell] ************************************************************************************************************************************************
changed: [10.156.0.2]

TASK [shell] ************************************************************************************************************************************************
 [WARNING]: Consider using the file module with state=absent rather than running 'rm'.  If you need to use command because file is insufficient you can add
'warn: false' to this command task or set 'command_warnings=False' in ansible.cfg to get rid of this message.

changed: [10.156.0.2]

PLAY RECAP **************************************************************************************************************************************************
10.156.0.2                 : ok=12   changed=7    unreachable=0    failed=0

root@instance-1:/etc/ansible# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                    NAMES
95209dbd8e8f        django:latest       "/bin/sh -c 'uwsgi -â¦"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp       django
222457df5feb        postgres:9.6.0      "/docker-entrypoint.â¦"   2 minutes ago        Up 2 minutes        0.0.0.0:5432->5432/tcp   postgresdb
