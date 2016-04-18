# PGConf 2016 Demo
Demo environment for my PGConf US 2016 Presentation [Deploying and Managing PostgreSQL with Ansible](http://www.pgconf.us/2016/event/158/deploying-and-managing-postgresql-with-ansible/)

## Requirements
* Ansible (tested with version 2.0.1.0)
* Vagrant (tested with version 1.8.1)
* Virtualbox (tested with version 4.3.32)

## Simple Demo

The Simple Demo environment will create 3 postgres instances with the same database and user installed on each one.  It's a quick way to see how Ansible modules can be used in a playbook.

## Full Demo

The Full Demo environment will create 2 postgres clusters with streaming replication, a barman instance for backup and recovery and a pgbouncer instance for session pooling and load balancing.
