# Install Cassandra Cluster Manager(CCM) 

Here you will install a virtualized Cassandra Multi Node Cluster on s single Ubuntu Machine.  This should
only be used for testing and not in production.

## Install Neccesary Python Packages

  sudo apt update

  sudo apt-get install python-pip

  sudo easy_install pyYaml

  sudo easy_install six

  pip install cassandra-driver

## Install Java-8

  sudo add-apt-repository ppa:webupd8team/java

  sudo apt update

  sudo apt install oracle-java8-set-default

## Install CCM

  pip install ccm

## Create test Cluster With Desired Cassandra Version

  ccm create -v 3.11.3 -n 3 my_cluster —vnodes

## Check Cluster and Start

  ccm list

  ccm status

  ccm start

  ccm status

## Dig Deeper into Status of Individual Nodes Specify the Node of Entry

  ccm node1 status

## Get a list of the Tokens Owned by Each Node

  ccm node1 ring

## Adding Nodes to a Cluster 

  ccm add node4 -i 127.0.0.4 -j 7400

  ccm status

  ccm node4 start

  ccm status

## Checkout the logs of node1

Look at the end of the log file to view gossip related info.  You should see the gossip protocol successfully taking place and the node joining the cluster.


  ccm node1 showlog


## Take one node down and take a look at the logs 

Look at the end of the log file to view gossip related info.  You should see the gossip protocol successfully taking place and the node leaving the cluster

  ccm node4 stop


## Bring node backup and check status

  ccm node4 start

  ccm node status

