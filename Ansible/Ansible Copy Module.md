# Task
There is data on jump host that needs to be copied on all application servers in Stratos DC. Nautilus DevOps team want to perform this task using Ansible. Perform the task as per details mentioned below:

a. On jump host create an inventory file /home/thor/ansible/inventory and add all application servers as managed nodes.

b. On jump host create a playbook /home/thor/ansible/playbook.yml to copy /usr/src/devops/index.html file to all application servers at location /opt/devops.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.
## Solution
Create the `inventory` file.
```sh
thor@jump_host ~$ cd ansible/
thor@jump_host ~/ansible$ vi inventory
```
```
stapp01 ansible_host=172.16.238.10 ansible_user=tony ansible_ssh_pass=Ir0nM@n
stapp02 ansible_host=172.16.238.11 ansible_user=steve ansible_ssh_pass=Am3ric@
stapp03 ansible_host=172.16.238.12 ansible_user=banner ansible_ssh_pass=BigGr33n
```
Create the playbook that copy file to all app servers.
```sh
thor@jump_host ~/ansible$ vi playbook.yml
```
```yml
- name: Copy file to all app servers
  hosts: all
  become: yes
  tasks:
  - name: Copy file
    copy:
      src=/usr/src/devops/index.html
      dest=/opt/devops/
```

Run the playbook.

```sh
thor@jump_host ~/ansible$ ansible-playbook -i inventory playbook.yml

PLAY [Copy file to all app servers] ********************************************

TASK [Gathering Facts] *********************************************************
ok: [stapp02]
ok: [stapp03]
ok: [stapp01]

TASK [Copy file] ***************************************************************
changed: [stapp01]
changed: [stapp03]
changed: [stapp02]

PLAY RECAP *********************************************************************
stapp01                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp02                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp03                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
## References

[Copy module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html)
