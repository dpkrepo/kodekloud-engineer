## Task
The Nautilus DevOps team is planning to test several Ansible playbooks on different app servers in Stratos DC. Before that, some pre-requisites must be met. Essentially, the team needs to set up a password-less SSH connection between Ansible controller and Ansible managed nodes. One of the tickets is assigned to you; please complete the task as per details mentioned below:

a. Jump host is our Ansible controller, and we are going to run Ansible playbooks through thor user from jump host.

b. There is an inventory file /home/thor/ansible/inventory on jump host. Using that inventory file test Ansible ping from jump host to App Server 3, make sure ping works.
## Solution


Ensure tahat inventory file has all needed value.

```
stapp01 ansible_host=172.16.238.10 ansible_ssh_pass=Ir0nM@n ansible_user=tony
stapp02 ansible_host=172.16.238.11 ansible_ssh_pass=Am3ric@ ansible_user=steve
stapp03 ansible_host=172.16.238.12 ansible_ssh_pass=BigGr33n ansible_user=banner
```

Generate keys for SSH connection.
```sh
thor@jump_host ~$ ssh-keygen -t rsa -b 2048
```

Copy the public key to App Server 3.
```sh
thor@jump_host ~$ ssh-copy-id banner@stapp03
```
Ping App Server 3 from Jump Host using Ansible.
```sh
thor@jump_host ~$ ansible -i ./ansible/inventory stapp03 -m ping
stapp03 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
```
## References

[How To Use The Ansible Ping Module](https://theitbros.com/how-to-use-ansible-ping-module/)
