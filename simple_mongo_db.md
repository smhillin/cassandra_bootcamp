## Install and Start Mongo DB

  sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
  
  echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee  /etc/apt/sources.list.d/mongodb-org-3.4.list

  sudo apt-get update

  sudo apt-get install -y mongodb-org

  sudo systemctl start mongod  
  sudo systemctl enable mongod

## Check ports in use

  netstat -plntu | grep 27017

27017 is the default port used by Mongodb server to listen for connections. 

## Check service status

  sudo service mongod status



## Run mongo shell

  mongo
 
## Create Collection

  use friends
  
## Insert into collection

  db.friends.insert({name:"shaun", email:"shaun@natvz.io"})
  
  db.friends.insert({name:"nadia", email:"nadia@gmail.com", age: '45', nationality: 'American'})
  

  
#### notice here that there is no need to define a schema because columns can be defined at runtime.  

## Practice adding documents

  1.  Add two 32 year old friends to the table that each have emails, age, nationality, and 2 other attributes.

  2.  Try and add a friend to the collection who doesn't have a  name but has an email.

  3.  Add a friend that has multiple email addresses?  How does this differ from RDBMS behavior?

## View all entrys in the Collection

  db.friends.find()
 
## Insert into Document

  db.friends.insert({name:"paul", email: "paul@gmail.com", age: '32', nationality: 'American', address: {street: '2304 vans way',   city: 'Beaumont', state: 'Texas'}})
  
db.friends.find({name:"paul"}) 


  
#### notice here no need for joins or multiple tables with foreign keys to represent rich nested data structure like the street address with multi dimensionality.
  
## Return All Friends from the Table with age=32

  db.friends.find()
  
  db.friends.find({age:"32"})
  

## Create new collection called pets and write multiple entries to the table

  use pets
  
  db.pets.insertMany([  
        {name:"Daisy", owner:"Mila", species:"dog", sex:"F",birth:"2007-02-22"},  
        {name:"Miss Bunny", owner:"Biljana", species:"rabbit", sex:"F",birth:"2007-12-09"},  
        {name:"Clyde", owner:"Dushan", species:"rabbit", sex:"M",birth:"2016-04-29"}])  
        
  db.pets.find({owner:"Dushan"})

## Update some data and add a 


  db.pets.update(
      { name: "Daisy"},
      {
          $set: { owner: "Shaun", status:"Crazy Chihuahua"}
      }
  )
  
## Practice

Return all the rabbits in the table

Return all the animals named Daisy
  
  
 #### notice that there is no primary key and queries can be made using any key
 
