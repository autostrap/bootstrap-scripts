Description
===========

This repository contains first-stage bootstrapping for Openstack instances. Its
purpose is to deploy the minimum required configuration repositories, generate
Hiera configuration (if applicable) and bootstrap an instance to the point
where it can either run Puppet standalone (i.e. from its own Hiera
configuration) or retrieve its configuration from a Puppet master.

Organization
============

This repository contains a range of standardized files and directories. Please
adhere to this organization when forking it to maintain compatibility with the
remaining components of our bootstrapping system. All paths

bin/
----

This directory contains scripts and other executables used in the course of the
bootstrapping process. *initialize_instance* includes it in its PATH variable
for easy use.

initialize_instance
-------------------

This is the first stage bootstrap script invoked by our default user-data
script. It logs its output to /var/log/initialize_instance.log.

metadata parameters
===================

Bootstrapping behaviour is governed by the following metadata parameters
(commonly passed from a Heat template):

project_classes
---------------

*type: boolean*

This parameter controls the addition of the following hierarchy entries in
hiera.yaml:

```
  - "project-config/nodes.d/%{::fqdn}"
  - "project-config/nodetypes.d/%{::nodetype}"
```

If project_classes is set to true, these entries are added to hiera.yaml, if it
is set to false they are omitted. This option should be set to true on a puppet
master or a node deployed through masterless puppet, and false on all puppet
agents. This prevents the classes array provided by the puppet master from
being used in puppet agents' early bootstrapping phase. If this parameter is
not present it is assumed to be false.

puppet_master
-------------

type: string (FQDN)

This parameter contains the fully qualified domain name of the puppet master,
puppet agents are retrieve their configuration from. This should be set on both
puppet agents and the puppet master, since the puppet master itself is usually
managed from the same source.

sys11_topics
------------

*Type: string (space delimited list)*

This parameter is  a space delimited list of configuration topics from
sys11-config to deploy. This is commonly used for early stage bootstrapping,
i.e. for getting a node to a point where it can act as a puppet agent or puppet
master.

