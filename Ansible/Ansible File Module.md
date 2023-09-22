# Task
The Nautilus DevOps team is working to test several Ansible modules on servers in Stratos DC. Recently they wanted to test the file creation on remote hosts using Ansible. Find below more details about the task:

a. Create an inventory file ~/playbook/inventory on jump host and add all app servers in it.

b. Create a playbook ~/playbook/playbook.yml to create a blank file /opt/app.txt on all app servers.

c. The /opt/app.txt file permission must be 0777.

d. The user/group owner of file /opt/app.txt must be tony on app server 1, steve on app server 2 and banner on app server 3.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml, so please make sure the playbook works this way without passing any extra arguments.
## Solution
Create the `inventory` file.
```sh
thor@jump_host ~$ cd playbook/
thor@jump_host ~/playbook$ vi inventory
```
```
stapp01 ansible_host=172.16.238.10 ansible_user=tony ansible_ssh_pass=Ir0nM@n
stapp02 ansible_host=172.16.238.11 ansible_user=steve ansible_ssh_pass=Am3ric@
stapp03 ansible_host=172.16.238.12 ansible_user=banner ansible_ssh_pass=BigGr33n
```
Create the playbook.
```sh
thor@jump_host ~/playbook$ vi playbook.yml
```
```yml
- name: Create a blank file
  hosts: all
  become: yes
  tasks:
    - name: Create the file
      file:
        path: /opt/app.txt
        mode: 0777
        owner: "{{ hostvars[inventory_hostname]['ansible_user'] }}"
        group: "{{ hostvars[inventory_hostname]['ansible_user'] }}"
        state: touch
```

Run the playbook.

```sh
hor@jump_host ~/playbook$ ansible-playbook -i inventory playbook.yml

PLAY [Create a blank file] *****************************************************

TASK [Gathering Facts] *********************************************************
ok: [stapp01]
ok: [stapp02]
ok: [stapp03]

TASK [Create the file] *********************************************************
changed: [stapp02]
changed: [stapp03]
changed: [stapp01]

PLAY RECAP *********************************************************************
stapp01                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp02                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp03                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```
## References

[Magic Variables](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_vars_facts.html#information-about-ansible-magic-variables)
