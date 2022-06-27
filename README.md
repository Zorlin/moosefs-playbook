moosefs-playbook
================

MooseFS on autopilot. Makes setting up, upgrading, maintaining and troubleshooting MooseFS a breeze.

Getting started
===============

Clone this repository somewhere handy
* git clone https://github.com/Zorlin/moosefs-playbook.git

Generate an SSH key if you don't already have one
* ssh-keygen

Copy your key to all the boxes you want to manage (replace localhost with the machine you want)
* ssh-copy-id localhost

Edit the inventory file. You will need at least one master and at least one chunkserver for a functional MooseFS installation. Three or more chunkservers are strongly recommended.

You should specify "moosefs_install_method" in your inventory file, but you can override it for each node.

Here's an example:

```
[all:vars]
moosefs_master_host = mfsmaster-lab
moosefs_install_method = package

[moosefs]
mfs-m01

[moosefs_master]
mfs-m01

[moosefs_metalogger]
mfs-m01

[moosefs_chunkserver]
mfs-m01
```

Install the required roles and do an Ansible run.

ansible-galaxy install -r roles/requirements.yml && ansible-playbook site.yml

Inventories
===========
Here are a list of included inventories.

* inventory is for testing purposes.

TODO
====

* rolling: Look into free_strategy

* rolling: Look into serial: "90%"

* rolling: https://stackoverflow.com/questions/49282094/ansible-define-playbook-default-vars-with-precedence-on-roles-but-overridable
  Allow overriding of strategy and serial using the inventory
