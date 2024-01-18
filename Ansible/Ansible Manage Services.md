## Task
Developers are looking for dependencies to be installed and run on Nautilus app servers in Stratos DC. They have shared some requirements with the DevOps team. Because we are now managing packages installation and services management using Ansible, some playbooks need to be created and tested. As per details mentioned below please complete the task:

a. On jump host create an Ansible playbook /home/thor/ansible/playbook.yml and configure it to install vsftpd on all app servers.

b. After installation make sure to start and enable vsftpd service on all app servers.

c. The inventory /home/thor/ansible/inventory is already there on jump host.

d. Make sure user thor should be able to run the playbook on jump host.

Note: Validation will try to run playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments.
## Solution

Create the playbook.yml file.

```yml
- name: Install vsftpd on all app servers
  hosts: all
  become: yes
  tasks:
    - name: Install vsftpd
      ansible.builtin.package:
        name: vsftpd
        state: present
    - name: Start vsftpd
      ansible.builtin.service:
        name: vsftpd
        state: started
    - name: Enable vsftpd
      ansible.builtin.service:
        name: vsftpd
        enabled: yes
```

## References

[ansible.builtin.package module – Generic OS package manager](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/package_module.html)

[ansible.builtin.service module – Manage services](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html)
