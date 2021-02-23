moosefs-playbook
================

MooseFS on autopilot. Makes setting up, upgrading, maintaining and troubleshooting MooseFS a breeze.

Doesn't yet support all features, but those needed for my personal MooseFS installation will be added as needed, and those I think are super cool probably even before them.

Getting started
===============

Clone this repository somewhere handy
* git clone https://github.com/Zorlin/scrutiny-playbook.git

Generate an SSH key if you don't already have one
* ssh-keygen

Copy your key to user "root" on all the boxes you want to manage (replace localhost with the machine you want)
* ssh-copy-id root@localhost

Edit the inventory file. You will need at least one master and at least one chunkserver for a functional MooseFS installation. Three or more chunkservers are strongly recommended.

You should specify "moosefs_install_method" (currently "package" or "build" are supported) in your inventory file, but you can override it for each node.

Here's an example:

```
[all:vars]
moosefs_master_host = mfsmaster-r01.windowpa.in
moosefs_install_method = package

[moosefs]
mfsmaster-r01.windowpa.in

[moosefs_master]
mfsmaster-r01.windowpa.in

[moosefs_metalogger]
mfsmaster-r01.windowpa.in

[moosefs_chunkserver]
mfsmaster-r01.windowpa.in
```

Install the required roles and do an Ansible run.

ansible-galaxy install -r roles/requirements.yml && ansible-playbook site.yml

Inventories
===========
Here are a list of included inventories.

* inventory is for testing purposes.

* inventory-production is an example of what I use in my homelab/Elastic NAS.

* inventory-sglab is the Windowpa.in MooseFS Lab in Singapore.

* inventory-regal is my toy lab used for developing this playbook safely.

TODO
====

* rolling: Look into free_strategy

* rolling: Look into serial: "90%"

* rolling: https://stackoverflow.com/questions/49282094/ansible-define-playbook-default-vars-with-precedence-on-roles-but-overridable
  Allow overriding of strategy and serial using the inventory
