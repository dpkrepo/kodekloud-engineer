## Task

The Nautilus DevOps team is practicing some of the Ansible modules and creating and testing different Ansible playbooks to accomplish tasks. Recently they started testing an Ansible file module to create soft links on all app servers. Below you can find more details about it.

Write a playbook.yml under /home/thor/ansible directory on jump host, an inventory file is already present under /home/thor/ansible directory on jump host itself. Using this playbook accomplish below given tasks:

Create an empty file /opt/dba/blog.txt on app server 1; its user owner and group owner should be tony. Create a symbolic link of source path /opt/dba to destination /var/www/html.

Create an empty file /opt/dba/story.txt on app server 2; its user owner and group owner should be steve. Create a symbolic link of source path /opt/dba to destination /var/www/html.

Create an empty file /opt/dba/media.txt on app server 3; its user owner and group owner should be banner. Create a symbolic link of source path /opt/dba to destination /var/www/html.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way without passing any extra arguments.

## Solution

Create the playbook.yml file.

```yml
- name: Create a file and a symbolic link on App Server 1
  hosts: stapp01
  become: yes
  tasks:
    - name: create a file
      ansible.builtin.file:
        path: /opt/dba/blog.txt
        state: touch
        owner: tony
        group: tony

    - name: Create a symbolic link
      ansible.builtin.file:
        src: /opt/dba
        dest: /var/www/html
        state: link

- name: Create a file and a symbolic link on App Server 2
  hosts: stapp02
  become: yes
  tasks:
    - name: create a file
      ansible.builtin.file:
        path: /opt/dba/story.txt
        state: touch
        owner: steve
        group: steve

    - name: Create a symbolic link
      ansible.builtin.file:
        src: /opt/dba
        dest: /var/www/html
        state: link

- name: Create a file and a symbolic link on App Server 3
  hosts: stapp03
  become: yes
  tasks:
    - name: create a file
      ansible.builtin.file:
        path: /opt/dba/media.txt
        state: touch
        owner: banner
        group: banner

    - name: Create a symbolic link
      ansible.builtin.file:
        src: /opt/dba
        dest: /var/www/html
        state: link
```

## References

[ansible.builtin.file module – Manage files and file properties](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html)
