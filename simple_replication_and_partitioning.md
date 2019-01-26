# Replication Factor on a Cassandra Cluster

## Create 4 Node CCM CLuster

https://github.com/smhillin/cassandra_bootcamp/blob/master/ccm_install.md


## Start CQL CLI

  ccm node1 cqlsh

## Create Keyspace with replication factor of 2

  CREATE KEYSPACE my_test WITH replication = {'class' : 'SimpleStrategy','replication_factor':2};

  use  my_test;

## Create Table with Primary key name

  CREATE TABLE students (name text, email text, PRIMARY KEY(name));
  
  DESCRIBE students;

## Insert Some Data into Table

  INSERT INTO students (name, email) VALUES ('shaun', 'shaun@natvz.io');

  INSERT INTO students (name, email) VALUES ('meghan', 'meghan@gmail.com');
  
  SELECT * FROM students;

## Exit to CLI and Examine Nodes for info

What is happening here?

  exit;
  
  ccm node1 json -k my_test -c students test; cat test;  
  ccm node2 json -k my_test -c students test; cat test;  
  ccm node3 json -k my_test -c students test; cat test;  

### Where is all the info?

## Flush Tables and then Dump node tables

  ccm flush
  
  ccm node1 json -k my_test -c students test; cat test;  
  ccm node2 json -k my_test -c students test; cat test;  
  ccm node3 json -k my_test -c students test; cat test;
  ccm node4 json -k my_test -c students test; cat test;


### How Many Copies does This Have? Is this conistent with replicaiton factor?


## Create Keyspace with replication factor of 3

  CREATE KEYSPACE my_test_3 WITH replication = {'class' : 'SimpleStrategy','replication_factor':3};

  use  my_test_3;

## Create Table with Primary key name

  CREATE TABLE amigos (name text, email text, PRIMARY KEY(name));
  
  DESCRIBE amigos;

## Insert Some Data into Table

  INSERT INTO amigos (name, email) VALUES ('shaun', 'shaun@natvz.io');

  INSERT INTO amigos (name, email) VALUES ('meghan', 'meghan@gmail.com');
  
  INSERT INTO amigos (name, email) VALUES ('george', 'george @gmail.com');
  
  SELECT * FROM amigos;

## Exit to CLI and Spend Some Time Examining Nodes for info

  ccm flush amigos

  ccm node1 json -k my_test_3 -c amigos test; cat test;  
  ccm node2 json -k my_test_3 -c amigos test; cat test;  
  ccm node3 json -k my_test_3 -c amigos test; cat test;
  ccm node4 json -k my_test_3 -c amigos test; cat test;
 
## Create Table with Primary key name

  DROP TABLE amigos;

  CREATE TABLE mates (first_name text , last_name text, PRIMARY KEY(first_name));
  
  INSERT INTO mates (first_name, last_name) VALUES ('John', 'Bonham');
'
  INSERT INTO mates (first_name, last_name) VALUES ('John', 'Lennon');
  
  INSERT INTO mates (first_name, last_name) VALUES ('Jimmy', 'Paige');
  
  INSERT INTO mates (first_name, last_name) VALUES ('Jimmy', 'Hendrix');
  
  SELECT * FROM mates
  
  ### what happens when two share the same primary key?  How can the issue be resolved

## Create Table with Compound Primary key first_name and last_name

  DROP TABLE mates;
  
  CREATE TABLE mates (first_name text , last_name text, PRIMARY KEY(first_name, last_name));
  
  DESCRIBE mates;
  
  INSERT INTO mates (first_name, last_name) VALUES ('John', 'Bonham');
'
  INSERT INTO mates (first_name, last_name) VALUES ('John', 'Lennon');
  
  INSERT INTO mates (first_name, last_name) VALUES ('Jimmy', 'Paige');
  
  INSERT INTO mates (first_name, last_name) VALUES ('Jimmy', 'Hendrix');
  
  SELECT * FROM mates
  
  
  
### is the primary key issue resolved?
  
## Exit to CLI, FLUSH tables Examine Nodes for info

Jot down each row that you inserted, and make note of what node they reside on. What is happening here?  Whats the replicaiton appear to be?

  exit;
  
  ccm flush
  
  ccm node1 json -k my_test_3 -c mates test; cat test;  
  ccm node2 json -k my_test_3 -c mates test; cat test;  
  ccm node3 json -k my_test_3 -c mates test; cat test;  
  ccm node4 json -k my_test_3 -c mates test; cat test;

### On what nodes is each row residing? How do the partition key and clustering key determine where and how the data is stored?

