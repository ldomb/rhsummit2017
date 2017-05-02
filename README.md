RH Summit 2017 Roles and Playbooks
=========

This repository hosts all playbooks and roles used for the button push RH MGMT demo done at RH Summit 2017.

Requirements
------------

- Ansible 2.2.1
- Ansible vault file in group_vars/all/vault
- Ansible Tower License
- Satelite 6 Manifest
- AWS cli
- Private key for ec2 instances
- CFME image for AWS

How is this executed
--------------

$ ansible-playbook buildrhmgmt.yaml --private-key=ldomb.pem --vault-password-file=../vaultpass -vv

A video of the full run can be found here: 
http://bit.ly/2oQwxxF

Dependencies
------------

All modules and dependencies can be found in this repository

Example Playbook
----------------

---
\- name: build ec2 instance<br>
&nbsp;&nbsp;  hosts: localhost<br>
&nbsp;&nbsp;  connection: local<br>
&nbsp;&nbsp;  gather_facts: false<br>
&nbsp;&nbsp;  user: root<br>

&nbsp;&nbsp;  vars_files: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    \- "group_vars/all/vars" <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   \- "group_vars/all/vault" <br>
&nbsp;&nbsp;  roles: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    \- { role: manage-ec2-instances } <br><br>

\- name: create tower <br>
&nbsp;&nbsp;  hosts: tag_Type_ansibletower <br>
&nbsp;&nbsp;  become: yes <br>
&nbsp;&nbsp;  remote_user: ec2-user <br>
&nbsp;&nbsp;  become_method: sudo <br>
&nbsp;&nbsp;  gather_facts: true <br>
&nbsp;&nbsp;  vars_files: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   \- "group_vars/all/vars" <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    \- "group_vars/all/vault" <br>
&nbsp;&nbsp;  roles: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    \- { role: buildansibletower } <br>


License
-------

GPL3

Author Information
------------------

Laurent Domb @ Red Hat Inc.
