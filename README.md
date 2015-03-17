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
