## Task
The Nautilus Application development team wanted to test some applications on app servers in Stratos Datacenter. They shared some pre-requisites with the DevOps team, and packages need to be installed on app servers. Since we are already using Ansible for automating such tasks, please perform this task using Ansible as per details mentioned below:

Create an inventory file /home/thor/playbook/inventory on jump host and add all app servers in it.

Create an Ansible playbook /home/thor/playbook/playbook.yml to install vim-enhanced package on all app servers using Ansible yum module.

Make sure user thor should be able to run the playbook on jump host.

Note: Validation will try to run playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments.
## Solution

Create the inventory file.
```
stapp01 ansible_host=172.16.238.10 ansible_ssh_pass=Ir0nM@n ansible_user=tony
stapp02 ansible_host=172.16.238.11 ansible_ssh_pass=Am3ric@ ansible_user=steve
stapp03 ansible_host=172.16.238.12 ansible_ssh_pass=BigGr33n ansible_user=banner
```

Create the playbook.

```yaml
---
- hosts: all
  tasks:
  - name: Install vim-enhanced package
    become: true
    ansible.builtin.yum:
      name: vim-enhanced
      state: present
```

Generate keys for SSH connection.

```sh
thor@jump_host ~$ ssh-keygen -t rsa -b 2048
```

Copy the public key to all App Servers.

```sh
thor@jump_host ~$ ssh-copy-id tony@stapp01
thor@jump_host ~$ ssh-copy-id steve@stapp02
thor@jump_host ~$ ssh-copy-id banner@stapp03
```

Run the playbook.

```sh
thor@jump_host ~/playbook$ ansible-playbook -i inventory playbook.yml

PLAY [all] *********************************************************************

TASK [Gathering Facts] *********************************************************
ok: [stapp02]
ok: [stapp03]
ok: [stapp01]

TASK [Install vim-enhanced package] ********************************************
changed: [stapp03]
changed: [stapp01]
changed: [stapp02]

PLAY RECAP *********************************************************************
stapp01                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp02                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp03                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```
## References

[yum module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/yum_module.html)
