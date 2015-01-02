ansible-simple-mesos
====================

This repository contains an 
[Ansible](http://www.ansible.com) playbook and roles for setting up a basic 
[Mesos](https://mesos.apache.org/)
cluster on CentOS 6.x hosts using the packages provided by
[Mesosphere](http://www.mesosphere.com). The overall workflow is modeled on the
[Mesosphere tutorial](http://mesosphere.com/docs/getting-started/datacenter/install/)
for setting up a Mesosphere cluster in the datacenter.

***Please note that these playbooks should NOT be considered production-ready!
These are experimental, and mostly represent the product of a bored afternoon
playing with Mesos and watching TableTop. :)***

Currently this playbook will set up 
[Zookeeper](https://zookeeper.apache.org/) and Mesos with 
[Marathon](https://github.com/mesosphere/marathon) and
[Chronos](https://github.com/airbnb/chronos) as installed frameworks, and
[Docker](https://www.docker.com/) installed on the worker nodes. An HDFS
filesystem is also set up. At some point
I hope to add [Hadoop MapReduce](https://github.com/mesos/hadoop),
[Spark](https://github.com/mesos/spark), and
[Torque](https://mesos.apache.org/documentation/running-torque-or-mpi-on-mesos/).

I tested it on a simple [Amazon EC2](http://aws.amazon.com/) cluster consisting
of six m1.small instances running a [RightScale](http://www.rightscale.com/) 
CentOS 6.5 image (ami-1c5dd974). I set it up with three masters (for HA) and three
worker nodes; a production cluster would obviously have more worker nodes than masters.

To use:
-------

1. Set up your cluster nodes with CentOS 6.x and make sure you can do passwordless
   SSH as root to all nodes from your workstation, or from wherever you plan to run Ansible.

2. Copy the `hosts.template` file to `hosts`. List an IP or hostname for each master
   node under the `[masters]` group, and each worker node under the `[workers]` group.

3. For each line of the `[masters]` group, include a unique `zkid=<number>` parameter
   to set the Zookeeper IDs.

4. If you want to assign "nice" hostnames, include a `setname=<hostname>` parameter
   for each host.

5. Run `ansible-playbook -i hosts cluster.yml`
