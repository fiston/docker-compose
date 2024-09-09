## Docker compose-Run multiple docker container

This repo articulates how to write Docker Compose file for running MongoDB and MongoExpress containers

### Key Components:-

- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

## Docker compose:-

Docker Compose is a tool that allows you to define and run multi-container Docker applications. It uses a YAML file to define the services that make up your application, and then starts and stops them all together with a single command.

### To run multiple Docker containers using Docker Compose, you'll need to follow these general steps:

Step 1: Define your application in a docker-compose.yml file: This file describes the services that make up your application, along with any necessary configuration options. For example, if your application consists of a web server and a database, your docker-compose.yml file might look something like this:

        version: '3'
    services:
      # my-app:
        # image: ${docker-registry}/my-app:1.0
        # ports:
         # - 3000:3000
      mongodb:
        image: mongo
        ports:
         - 27017:27017
        environment:
         - MONGO_INITDB_ROOT_USERNAME=admin
         - MONGO_INITDB_ROOT_PASSWORD=password
        volumes:
         - mongo-data:/data/db
      mongo-express:
        image: mongo-express
        restart: always
        ports:
         - 8080:8081
        environment:
         - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
         - ME_CONFIG_MONGODB_ADMINPASSWORD=password
         - ME_CONFIG_MONGODB_SERVER=mongodb
        depends_on:
         - "mongodb"
    volumes:
      mongo-data:
        driver: local

### With Docker Compose

#### Start your application: To start your application, run the following command from the directory where your docker-compose.yml file is located:

Step 1: start mongodb and mongo-express

    docker-compose -f docker-compose.yaml up
    
_You can access the mongo-express under localhost:8080 from your browser_
    
Step 2: in mongo-express UI - create a new database "my-db"

Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"       
    
Step 4: start node server 

    cd app
    npm install
    node server.js
    
Step 5: access the nodejs application from browser 

    http://localhost:3000

#### To build a docker image from the application

    docker build -t my-app:1.0 .       
    
The dot "." at the end of the command denotes location of the Dockerfile.
