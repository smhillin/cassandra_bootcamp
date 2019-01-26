# Cassandra materialized views

## Create Source Table

Here pid generated a unique primary id for each player.

  CREATE TABLE players_mv (pid UUID PRIMARY KEY, name text, age int, team text);
  
## Insert players

  INSERT INTO players_mv (pid,name, age, team) VALUES (uuid(),'Mo Salah', 26, 'Liverpool');
  INSERT INTO players_mv (pid,name, age, team) VALUES (uuid(),'Sadio Mane', 26, 'Liverpool');
  INSERT INTO players_mv (pid,name, age, team) VALUES (uuid(),'Kylian Mbappe', 20, 'PSG');
  INSERT INTO players_mv (pid,name, age, team) VALUES (uuid(),'Neymar', 26, 'PSG');
  
  SELECT * FROM players_mv;
  
## Now try a filter query by team.  What happens?

  SELECT team, name, age FROM player_mv WHERE team = 'Liverpool';

## Create a materlized view for players by country.  

  CREATE MATERIALIZED VIEW player_by_team 
  AS SELECT name, age, team 
  FROM players_mv 
  WHERE team IS NOT NULL AND pid IS NOT NULL 
  PRIMARY KEY (team, pid);

## Because the new materialized view is partitioned by 
team, it supports queries based on the players team. Try it

  SELECT team, name, age FROM player_by_team WHERE team = 'Liverpool';
 
Why is the prefered over secondary indexes?
  
## Create a materlialized view that support the following query

  SELECT team, name, age FROM player_by_team WHERE age = 26;
