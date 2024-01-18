## Task

There are some files that need to be created on all app servers in Stratos DC. The Nautilus DevOps team want these files to be owned by user root only however, they also want that the app specific user to have a set of permissions on these files. All tasks must be done using Ansible only, so they need to create a playbook. Below you can find more information about the task.

Create a playbook named playbook.yml under /home/thor/ansible directory on jump host, an inventory file is already present under /home/thor/ansible directory on Jump Server itself.

Create an empty file blog.txt under /opt/dba/ directory on app server 1. Set some acl properties for this file. Using acl provide read '(r)' permissions to group tony (i.e entity is tony and etype is group).

Create an empty file story.txt under /opt/dba/ directory on app server 2. Set some acl properties for this file. Using acl provide read + write '(rw)' permissions to user steve (i.e entity is steve and etype is user).

Create an empty file media.txt under /opt/dba/ on app server 3. Set some acl properties for this file. Using acl provide read + write '(rw)' permissions to group banner (i.e entity is banner and etype is group).

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way, without passing any extra arguments.
## Solution

Create the playbook.yml file.

```yml
- name: Create an empty file and set some acl properties on App Server 1
  hosts: stapp01
  become: yes
  tasks:
    - name: Create an empty file
      ansible.builtin.file:
        path: /opt/dba/blog.txt
        state: touch
        owner: root
    - name: set some acl properties
      ansible.posix.acl:
        path: /opt/dba/blog.txt
        entity: tony
        etype: group
        permissions: r
        state: present

- name: Create an empty file and set some acl properties on App Server 2
  hosts: stapp02
  become: yes
  tasks:
    - name: Create an empty file
      ansible.builtin.file:
        path: /opt/dba/story.txt
        state: touch
        owner: root
    - name: set some acl properties
      ansible.posix.acl:
        path: /opt/dba/story.txt
        entity: steve
        etype: user
        permissions: rw
        state: present


- name: Create an empty file and set some acl properties on App Server 3
  hosts: stapp03
  become: yes
  tasks:
    - name: Create an empty file
      ansible.builtin.file:
        path: /opt/dba/media.txt
        state: touch
        owner: root
    - name: set some acl properties
      ansible.posix.acl:
        path: /opt/dba/media.txt
        entity: banner
        etype: group
        permissions: rw
        state: present
```

## References

[ansible.posix.acl module – Set and retrieve file ACL information](https://docs.ansible.com/ansible/latest/collections/ansible/posix/acl_module.html)
