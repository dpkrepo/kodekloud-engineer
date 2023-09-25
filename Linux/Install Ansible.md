# Task
During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with Ansible for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.

Install ansible version 4.7.0 on Jump host using pip3 only. Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.
## Solution
Install Ansible version 4.7.0 using pip3 globally.
```sh
thor@jump_host ~$ sudo pip3 install ansible==4.7.0
```
## References

[Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
