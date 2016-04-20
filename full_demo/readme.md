#Vagrant PostgreSQL

##Requirements

* Ansible (tested with version 2.0.1.0)
* Vagrant (tested with version 1.8.1)
* Virtualbox (tested with version 4.3.32)

##Create and Provision VMs

There's some issues running the standard `vagrant up` command since we need all VMs available before running the Ansible playbook to provision them.  Vagrant will also provision each VM individually, but we are overriding this by allowing ansible to run against all hosts.  Run these commands to create the PostgreSQL environment:

```
vagrant up --no-provision
vagrant provision pg-a-1
```

##Connecting to Databases

**Database names and usernames are defined in `provisioning/group_vars/cluster_a[b]`**

Connect to pg-a-1:

`psql -h 127.0.0.1 -p 7001 -d <dbname> -U <username>`

Connect to pg-a-2:
`psql -h 127.0.0.1 -p 7002 -d <dbname> -U <username>`

Connect to pg-b-1:

`psql -h 127.0.0.1 -p 7003 -d <dbname> -U <username>`

Connect to pg-b-2:
`psql -h 127.0.0.1 -p 7004 -d <dbname> -U <username>`

Connect through PGBouncer:
`psql -h 127.0.0.1 -p 8001 -d <dbname> -U <username>`


##Testing Failover

On current master run `pg_ctl stop -m immediate`

Promote standby by running `pg_ctl promote`

Edit Vagrantfile:

```
"master" => ["pg-a-2"],
"standby" => ["pg-a-1"],
```

Provision VMs again

```
vagrant provision pg-a-1
ansible-playbook pg-config.yml
```
