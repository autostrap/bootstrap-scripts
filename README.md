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

additional.d/
-------------

This directory contains files to be supplied as *additional_script* metadata
entry via Heat. If this metadata entry is set, the *initialize_instance* script
will call the script thus specified once it is finished. Currently it contains
the following scripts:

  * *deploy_puppet_masterless* - Deploys a self-contained puppet setup that uses
    hiera configuration on the local machine.

  * *deploy_puppet_agent* - Deploys a puppet agent configured by the puppet
    whose host name is specified via the cloud-config metadata entry
    *puppet_master*.

bin/
----

This directory contains scripts and other executables used in the course of the
bootstrapping process. *initialize_instance* includes it in its PATH variable
for easy use.

initialize_instance
-------------------

This is the first stage bootstrap script invoked by our default user-data
script. It logs its output to /var/log/initialize_instance.log.
