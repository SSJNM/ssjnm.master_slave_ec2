Role - Master Slave EC2
=========

The role intends to launch Master and Slave nodes in AWS Cloud for Multi-Node clusters in K8s , Hadoop and other technonogies 

Requirements
------------

- Needs python-3.6+ with *boto* library installed in your system
- Should have pre created private keys to be used during the launch of Instances
- The role expects that either you have exported the environment variables *AWS_ACCESS_KEY_ID* and *AWS_SECRET_ACCESS_KEY*

Role Variables
--------------

There are some necessary variable that needs to be defined before using this role
Other variable that may be changed in future are also attached with (*defaults/main.yml*)

**Necessary variables:**
1) aws_master_key_name: This variable needs the name of private key to be given access for master
Example --> aws_master_key_name : yourmasterkey

2) aws_slaves_key_name: This variable needs the name of private key to be given access for slaves
Example --> aws_slaves_key_name : yourslavekey

3) your_subnet_id: This variables needs the subnet-id of subnet where you want to launch the Instances

**Default variables:** These variables are not neccesary to be passed and will accept default values when nothing passed in var_file

Normally we want only a single master node so we are using single node for master
master_node_count: No. of master Nodes
slaves_node_count: No. of slave Nodes

ami_id: Pass the AMI-ID to be used

It is recommended to use instance type better than t2.micro to avoid any setup failure
master_instance_type: Instance type for Master
slaves_instance_type: Instance type for Slaves

The default name for master node and slave nodes
master_node_name: Name tag for Master Instance
slave_nodes_name: Name tag for Slave Instances

Considering I live in India so Mumbai is the nearest datacenter
region: The region of AWS Datacenter to be used
Ex --> region: ap-south-1

Dependencies
------------

None

Example Playbook
----------------

Launching one Master and four Slave Nodes with the attachment of aws_cloud_key on the subnet with subnet-id subnet-12345abcd 

    - hosts: all
      vars:
        aws_master_key_name: aws_cloud_key
        aws_slaves_key_name: aws_cloud_key
        your_subnet_id: subnet-12345abcd
        slaves_node_count:4 
      roles:
         - role: ssjnm.master_slave_ec2

Author Information
------------------

This role was created by Nishant Singh, GitHub User - SSJNM
