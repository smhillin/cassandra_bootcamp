## Create a 4 node Cassandra Cluster and go to cqli

  ccm <node> cqlsh

## Create a Keyspace with a Replication factor of 3

  CREATE KEYSPACE con_lab WITH replication = {'class' : 'SimpleStrategy','replication_factor':3};
  
  USE con_lab;


## Create a new table

  CREATE TABLE students (name text, email text, PRIMARY KEY(name));

  DESCRIBE students;

## Insert some data into table

  INSERT INTO students (name, email) VALUES ('shaun', 'shaun@natvz.io');

  INSERT INTO students (name, email) VALUES ('meghan', 'meghan@gmail.com');

  INSERT INTO students (name, email) VALUES ('Mo', 'mohamed@natvz.io');

  INSERT INTO students (name, email) VALUES ('Lynn', 'lynn@gmail.com');

SELECT * FROM students;


## Check Consistency Level

  CONSISTENCY

## Set consistency level to 1 if not already so

  CONSISTENCY ONE;

## Select Statement

  SELECT * FROM students;

you should recieve a table

## change Consistency to Quorum 

  CONSISTENCY QUORUM;
  
## Query Tables
  
  SELECT * from students;

## Exit from cql and kill 1 nodes

  ccm <node-1> stop ;
  
## return to cql cli and your keyspace(make sure you use a running node)

  ccm <node> cqlsh;
  
## change Consistency to Quorum  

  CONSISTENCY QUORUM;
  
## Query Tables
  
  SELECT * from students;
  
Were you able to query the table?  What happened?  Try starting back up your node and then running the query.
  
  
  
