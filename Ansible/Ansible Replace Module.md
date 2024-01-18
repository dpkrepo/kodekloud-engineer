## Task

There is some data on all app servers in Stratos DC. The Nautilus development team shared some requirement with the DevOps team to alter some of the data as per recent changes they made. The DevOps team is working to prepare an Ansible playbook to accomplish the same. Below you can find more details about the task.

Write a playbook.yml under /home/thor/ansible on jump host, an inventory is already present under /home/thor/ansible directory on Jump host itself. Perform below given tasks using this playbook:

We have a file /opt/dba/blog.txt on app server 1. Using Ansible replace module replace string xFusionCorp to Nautilus in that file.

We have a file /opt/dba/story.txt on app server 2. Using Ansiblereplace module replace the string Nautilus to KodeKloud in that file.

We have a file /opt/dba/media.txt on app server 3. Using Ansible replace module replace string KodeKloud to xFusionCorp Industries in that file.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.

## Solution

Create the playbook.yml file.

```yml
- name: Replace string on App Server 1
  hosts: stapp01
  become: yes
  tasks:
    - name: Replace string
      ansible.builtin.replace:
        path: /opt/dba/blog.txt
        regexp: xFusionCorp
        replace: Nautilus


- name: Replace string on App Server 2
  hosts: stapp02
  become: yes
  tasks:
    - name: Replace string
      ansible.builtin.replace:
        path: /opt/dba/story.txt
        regexp: Nautilus
        replace: KodeKloud

- name: Replace string on App Server 3
  hosts: stapp03
  become: yes
  tasks:
    - name: Replace string
      ansible.builtin.replace:
        path: /opt/dba/media.txt
        regexp: KodeKloud
        replace: "xFusionCorp Industries"
```

## References

[ansible.builtin.replace module – Replace all instances of a particular string in a file using a back-referenced regular expression](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/replace_module.html)
