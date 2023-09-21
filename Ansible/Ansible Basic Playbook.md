# Task

One of the Nautilus DevOps team members was working on to test an Ansible playbook on jump host. However, he was only able to create the inventory, and due to other priorities that came in he has to work on other tasks. Please pick up this task from where he left off and complete it. Below are more details about the task:


The inventory file /home/thor/ansible/inventory seems to be having some issues, please fix them. The playbook needs to be run on App Server 2 in Stratos DC, so inventory file needs to be updated accordingly.


Create a playbook /home/thor/ansible/playbook.yml and add a task to create an empty file /tmp/file.txt on App Server 2.


Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.
## Solution

Edit inventory file.
```sh
thor@jump_host ~$ vi /home/thor/ansible/inventory
```
```
stapp02 ansible_host=172.16.238.11 ansible_user=steve ansible_ssh_pass=Am3ric@ ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

Create a playbook to create a empty file.
```sh
thor@jump_host ~$ vi /home/thor/ansible/playbook.yml
```


```yml
- name: Create empty file
  hosts: stapp02
  become: yes
  tasks:
    - name: Create the file
      file:
        path: /tmp/file.txt
        state: touch
```

Check current content of /tmp/ directory on stapp02 server.
```sh
thor@jump_host ~$ cd ansible/
```

```sh
thor@jump_host ~/ansible$  ansible all -a "ls -ltr /tmp/" -i inventory
stapp02 | CHANGED | rc=0 >>
total 12
-rwx------ 1 root  root   701 Feb  7  2023 ks-script-l36mq90h
-rwx------ 1 root  root   291 Feb  7  2023 ks-script-kzk1nzfd
drwx------ 2 steve steve 4096 Sep 21 21:49 ansible_ansible.legacy.command_payload_26pstnxy
```

Run playbook.

```sh
thor@jump_host ~/ansible$ ansible-playbook -i inventory playbook.yml

PLAY [Create empty file] ***********************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************
ok: [stapp02]

TASK [Create the file] *************************************************************************************************************************************************************
changed: [stapp02]

PLAY RECAP *************************************************************************************************************************************************************************
stapp02                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```

`file.txt` was successfully created on stapp02 in /tmp/ directory.
```sh
thor@jump_host ~/ansible$ ansible all -a "ls -ltr /tmp/" -i inventory
stapp02 | CHANGED | rc=0 >>
total 12
-rwx------ 1 root  root   701 Feb  7  2023 ks-script-l36mq90h
-rwx------ 1 root  root   291 Feb  7  2023 ks-script-kzk1nzfd
-rw-r--r-- 1 root  root     0 Sep 21 21:52 file.txt
drwx------ 2 steve steve 4096 Sep 21 21:52 ansible_ansible.legacy.command_payload_vp3zan85
```

## References

[Build inventory](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#inventory-basics-formats-hosts-and-groups)

[Manage files and file properties](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html)

