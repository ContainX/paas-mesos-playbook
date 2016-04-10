# paas-mesos-playbook

This is a playbook which I use for deploying clusters utilizing the following technologies:

- Oracle Java 8 for Zookeeper and Marathon
- Apache Mesos w/ Zookeeper for Cluster Scheduling
- Mesosphere Marathon for long running task and Docker support
- Docker for containers
- Weave for multi-host Docker networking and DNS resolution

This playbook supports 1..N Mesos Master nodes and 1..N Mesos slave based nodes.

## Using this playbook with Vagrant

Out of the box after cloning this repo a simple ```vagrant up``` will create a single Master and 2 Slave cluster.  This cluster will create a weave network for docker to docker multi-host networking with a DNS name of *.mycompany.local.  

#### To customize the number of slaves and attribution

1. Modify the ```vagrant``` file to reflect the desired number of slave nodes and any slave attribution.  This file contains comments and examples to get you started
2. Modify the ```VagrantFile``` and change the ```num_slaves``` value to be the number of slaves you created in the vagrant file.
3. Add any custom options in the ```masters.yml``` and ```slaves.yml``` .
4. Run ```vagrant up```
