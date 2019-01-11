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

  use my_test
  
## Insert into Document

  db.users.insert({name:"shaun", email:"shaun@natvz.io"})
  
  db.users.insert({name:"nadia", email:"nadia@gmail.com", age: '45', nationality: 'American'})
  
  db.users.insert({name:"paul", email:"paul@gmail.com", age: '32', nationality: 'American', address: {street: '2304 vans way', city: 'Beaumont', state: 'Texas'})
  
  notice here that there is no need to create a table and also columns can be created at runtime.
  
## Return All Results from Table

  db.users.find()
