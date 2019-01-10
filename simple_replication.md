# Replication Factor on a Cassandra Cluster

## Start CQL CLI

  ccm node1 cqlsh

## Create Keyspace

  CREATE KEYSPACE my_test WITH replication = {‘class' : ‘SimpleStrategy’,’replication_factor’:2};

  use  my_test

## Create Table

  CREATE TABLE students (name text, email text, PRIMARY KEY(name));

## Insert Some Data into Table

  INSERT INTO students (name, email) VALUES ('shaun', 'shaun@natvz.io’);

  INSERT INTO students (name, email) VALUES ('meghan', 'meghan@gmail.com’);

## Exit to CLI and Flush Tables

What is happening here?

  exit;

  ccm flush

## Dump node tables to view what is on each node

How Many Copies does This Have?

Is this conistent with replicaiton factor?

  ccm node1 json -k my_test -c students test; cat test;
  ccm node2 json -k my_test -c students test; cat test;
  ccm node3 json -k my_test -c students test; cat test;
