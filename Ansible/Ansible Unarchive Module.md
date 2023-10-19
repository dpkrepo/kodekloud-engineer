## Task
One of the DevOps team members has created a zip archive on jump host in Stratos DC that needs to be extracted and copied over to all app servers in Stratos DC itself. Because this is a routine task, the Nautilus DevOps team has suggested automating it. We can use Ansible since we have been using it for other automation tasks. Below you can find more details about the task:

We have an inventory file under /home/thor/ansible directory on jump host, which should have all the app servers added already.

There is a zip archive /usr/src/dba/devops.zip on jump host.
## Solution

Write the playbook.
```yaml
- hosts: all
  become: true
  tasks:
    - name: Unzip /usr/src/dba/devops.zip archive in /opt/dba/
      ansible.builtin.unarchive:
        src: /usr/src/dba/devops.zip
        dest: /opt/dba/
        owner: "{{ ansible_user }}"
        group: "{{ ansible_user }}"
        mode: 0755
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
ok: [stapp02]
ok: [stapp01]
ok: [stapp03]

TASK [Unzip /usr/src/dba/devops.zip archive in /opt/dba/] **********************
changed: [stapp02]
changed: [stapp01]
changed: [stapp03]

PLAY RECAP *********************************************************************
stapp01                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp02                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
stapp03                    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```
## References

[unarchive module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/unarchive_module.html)
