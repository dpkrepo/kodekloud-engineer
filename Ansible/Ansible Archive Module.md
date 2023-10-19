## Task
The Nautilus DevOps team has some data on each app server in Stratos DC that they want to copy to a different location. However, they want to create an archive of the data first, then they want to copy the same to a different location on the respective app server. Additionally, there are some specific requirements for each server. Perform the task using Ansible playbook as per requirements mentioned below:

Create a playbook named playbook.yml under /home/thor/ansible directory on jump host, an inventory file is already placed under /home/thor/ansible/ directory on Jump Server itself.

Create an archive blog.tar.gz (make sure archive format is tar.gz) of /usr/src/sysops/ directory ( present on each app server ) and copy it to /opt/sysops/ directory on all app servers. The user and group owner of archive blog.tar.gz should be tony for App Server 1, steve for App Server 2 and banner for App Server 3.

Note: Validation will try to run playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments.
## Solution

Create the playbook file.
```yaml
- hosts: all
  tasks:
    - name: zip /usr/src/sysops/ directory
      become: true
      community.general.archive:
        path: /usr/src/sysops
        dest: /opt/sysops/blog.tar.gz
        format: gz
        owner: "{{ ansible_user }}"
        group: "{{ ansible_user }}"
```

Generate keys for SSH connection.

```sh
thor@jump_host ~/ansible$ ssh-keygen -t rsa -b 2048
```

Copy public key to App Servers.

```sh
thor@jump_host ~/ansible$ ssh-copy-id tony@stapp01
thor@jump_host ~/ansible$ ssh-copy-id steve@stapp02
thor@jump_host ~/ansible$ ssh-copy-id banner@stapp03
```

Run the playbook.
```sh
thor@jump_host ~/ansible$ ansible-playbook -i inventory playbook.yml

PLAY [all] *********************************************************************

TASK [Gathering Facts] *********************************************************
ok: [stapp02]
ok: [stapp01]
ok: [stapp03]

TASK [zip /usr/src/sysops/ directory] ******************************************
changed: [stapp03]
changed: [stapp01]
changed: [stapp02]

PLAY RECAP *********************************************************************
stapp01                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp02                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp03                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```
## References

[archive module](https://docs.ansible.com/ansible/latest/collections/community/general/archive_module.html)
