## Update and Upgrade each instance

`
sudo apt upgrade && sudo apt upgrade -y
`

## Check for Java and Python Version and Install

You should have Java 8 if Not Install

`
java —version
`

`
sudo add-apt-repository ppa:webupd8team/java
`

`
sudo apt-get update
`

`
sudo apt-get install oracle-java8-set-default
`

`
java —version
`

You should have python 3.  If not Install

`
python3 —version
`

`
sudo apt-get python3
`

## Install Cassandra

### Add the Apache Repo to /etc/apt/sources.list.d/cassandra.sources.list.

`
echo "deb http://www.apache.org/dist/cassandra/debian 311x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
`

### Add the Apache Cassandra Keys

`
sudo curl https://www.apache.org/dist/cassandra/KEYS | sudo apt-key add -
`

### Update Repos

`
sudo apt-get update
`

### Install Cassandra

`
sudo apt-get install cassandra
`

### Goto Cassandra conf Directory

`
cd /etc/cassandra
`

### Take backup of main configuration file before you make any change in it.

`
sudo cp cassandra.yaml cassandra.yaml.bak
`

## Make Configuration Changes to Yaml File

### Goto Cassandra conf Directory.

`
cd /etc/cassandra
sudo rm cassandra.yaml
`

### Open cassandra.yaml in your favorite editor and edit below parameters as mentioned below

    cluster_name: ‘My Cluster’
    authenticator: PasswordAuthenticator (optional)
    seeds: “<node1_private_ip_address>,<node2_private_ip_address>,<node3_private_ip_address>”
    listen_address:<node_private_ip_address>
    rpc_address: 0.0.0.0
    broadcast_rpc_address:<node_private_ip_address>
    endpoint_snitch: Ec2Snitch

### Save the file


## Start up Cassandra node

### Clear the default data from the Cassandra system table in order to import the new values set in the cassandra.yaml config file:

`
sudo rm -rf /var/lib/cassandra/data/system/*
`

### Start Cassandra Service on that node.

`
sudo service cassandra start
`

### Wait for 10 second and check cluster status.

`
sudo nodetool status
`

### After all 3 nodes have been bootstrapped you should see all 3 appear here


    Datacenter: us-west-2
    Status=Up/Down
    |/ State=Normal/Leaving/Joining/Moving
    --  Address        Load       Tokens       Owns (effective)  Host ID                               Rack
    UN  172.31.29.158  185.9 KiB  256          67.3%             eaaa4c0d-59d5-4197-a450-40c40c534799  2a
    UN  172.31.25.233  160.39 KiB  256          63.6%             e16dcfdd-aa36-4745-b57b-c05ac3902173  2a
    UN  172.31.34.131  160.67 KiB  256          69.1%             3de3304b-ed6d-4873-8493-a10cdc497ab3  2b


## Helpful commands

### Upload from Desktop to EC2

Change permissions on cassandra directory

`
sudo chown -R ubuntu:ubuntu /etc/cassandra
`

On local machine
`
scp -i cass_test.pem <local_path_to_yaml> ubuntu@54.184.54.21:/etc/cassandra/cassandra.yaml
`

### Uninstall Cassandra

`
sudo apt-get remove cassandra
`

`
sudo rm -rf /var/lib/cassandra && sudo rm -rf /var/log/cassandra && sudo rm -rf /etc/cassandra
`


