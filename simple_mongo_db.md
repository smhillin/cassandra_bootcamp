## Install and Start Mongo DB

  sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6

  sudo apt-get update

  sudo apt-get install -y mongodb-org

  sudo systemctl start mongod
  sudo systemctl enable mongod

## Check ports in use

  netstat -plntu | grep 27017

## Check service status
  sudo service mongod status

27017 is the default port used by Mongodb server to listen for connections. 

## Run mongo shell

  mongo
 
## Create DB

  use friends
  
## Insert into Document

  db.friends.insert({name:"shaun", email:"shaun@natvz.io"})
  
  db.friends.insert({name:"nadia", email:"nadia@gmail.com", age: '45', nationality: 'American'})
  
notice here that there is no need to create a collection and also columns can be created at runtime.  No need to create multiple 
tables to 
  
## Insert into Document

  db.friends.insert({name:"paul", email:"paul@gmail.com", age: '32', nationality: 'American', address: {street: '2304 vans way',   city: 'Beaumont', state: 'Texas'}})
  
notice here no need for joins or multiple tables with foreign keys to represent rich data structure with multi dimensionality.
  
## Return All Results from Table

  db.users.find()
  

## Create new table and write multiple entries
'
  use pets
  
  db.pets.insertMany([
    {name:"Daisy", owner:"Mila", species:"dog", sex:"F",birth:"2007-02-22"},
    {name:"Miss Bunny", owner:"Biljana", species:"rabbit", sex:"F",birth:"2007-12-09"},
    {name:"Clyde", owner:"Dushan", species:"rabbit", sex:"M",birth:"2016-04-29"}])

  db.pets.find({owner:"Dushan")})
'
## Update some data


  db.pets.update(
      { name: "Daisy"},
      {
          $set: { owner: "Shaun", status:"Crazy Chihuahua"}
      }
  )
  
  db.pets.find({species:"rabbit"})
  
  db.pets.find({name:"Daisy"})
  
 notice that there is no primary key and queries can be made using any key
 
