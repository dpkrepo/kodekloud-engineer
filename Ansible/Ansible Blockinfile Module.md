## Task
The Nautilus DevOps team wants to install and set up a simple httpd web server on all app servers in Stratos DC. Additionally, they want to deploy a sample web page for now using Ansible only. Therefore, write the required playbook to complete this task. Find more details about the task below.

We already have an inventory file under /home/thor/ansible directory on jump host. Create a playbook.yml under /home/thor/ansible directory on jump host itself.

Using the playbook, install httpd web server on all app servers. Additionally, make sure its service should up and running.

Using blockinfile Ansible module add some content in /var/www/html/index.html file. Below is the content:

Welcome to XfusionCorp!

This is Nautilus sample file, created using Ansible!

Please do not modify this file manually!

The /var/www/html/index.html file's user and group owner should be apache on all app servers.

The /var/www/html/index.html file's permissions should be 0644 on all app servers.

Note:

i. Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.

ii. Do not use any custom or empty marker for blockinfile module.
## Solution
Write a playbook.

```yaml
- hosts: all
  become: true
  tasks:
    - name: Install httpd
      ansible.builtin.yum:
        name: httpd
        state: present
    - name: Start service httpd, if not started
      ansible.builtin.service:
        name: httpd
        state: started
    - name: Add content to /var/www/html/index.html
      ansible.builtin.blockinfile:
        path: /var/www/html/index.html
        create: true
        block: |
          Welcome to XfusionCorp!
          This is Nautilus sample file, created using Ansible!
          Please do not modify this file manually!
        owner: apache
        group: apache
        mode: 0644
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
thor@jump_host ~/ansible$ ansible-playbook -i inventory playbook.yml

PLAY [all] *********************************************************************

TASK [Gathering Facts] *********************************************************
ok: [stapp01]
ok: [stapp02]
ok: [stapp03]

TASK [Install httpd] ***********************************************************
ok: [stapp02]
ok: [stapp03]
ok: [stapp01]

TASK [Start service httpd, if not started] *************************************
ok: [stapp03]
ok: [stapp02]
ok: [stapp01]

TASK [Add content to /var/www/html/index.html] *********************************
changed: [stapp03]
changed: [stapp02]
changed: [stapp01]

PLAY RECAP *********************************************************************
stapp01                    : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp02                    : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp03                    : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```
## References

[blockinfile module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/blockinfile_module.html)
