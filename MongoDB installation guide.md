# MongoDB Installation Guide

This guide will walk you through the installation of MongoDB on an Ubuntu system.

## Method-1:- Installing MongoDB directly from the terminal

## Step 1: Import the MongoDB GPG Key

First, import the MongoDB public GPG key:

```
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
```

## Step 2: Create a List File for MongoDB

Create the **/etc/apt/sources.list.d/mongodb-org-6.0.list** file for MongoDB:

```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

## Step 3: Update the local package database:
```
sudo apt-get update
```

## Step 4: Install the MongoDB packages
```
sudo apt-get install -y mongodb-org
```

## Step 5: Start the MongoDB service:
```
sudo systemctl start mongod
```
note:- In this step the start command does not work properly. So to verify whether its successfully installed, follow the step-6.

## Step 6: Verify MongoDB Installation
```
sudo systemctl status mongod
```

note:- After executing the above command, you will be getting a status whether its running properly or not. If its highlighted in green,then MongoDB is properly installed.

## Step 7: Install Mongosh
To interact with MongoDB, install mongosh (the MongoDB shell):
```
sudo apt-get install -y mongodb-mongosh
```

## Step 8: Run the mongosh
Run the command "mongosh" in the terminal
```
mongosh
```

note:- Since the Step-4 dosent work properly,you can directly interact with mongosh and do the queries.

## Step 9: Check the available databases
Use "show dbs" command to check the available databases. 
```
show dbs
```
note:- The initial databases are system databases where the system collections are stored.

## Some important point to consider:

1.After installing the MongoDB by folllowing those steps, it is advised to create a seperate database.As mentioned in step-9 you wont be having the access to alter the collection.

2.To create a new database,first open the "mongosh" in the terminal and use the command **use database name**. This command will automatically create a new database if it's not existed already.
```
use <databasename>
```
   
3.Open the browser and navigate to **MongoDB Atlas**.After logging in, then create a cluster. This is very crucial for monitoring aspects such as the insertion, updation or deletion of documents. It will also be helpful for doing similarity search.  

## Method-2:- Installing MongoDB through docker

## Step-1: Install docker desktop 
Install the docker desktop by refereing this [docker-installation-link](https://docs.docker.com/desktop/install/ubuntu/)

## Step-2: Check the context of docker
```
docker context list
```
note:- You will be seeing **default and docker-desktop** as the context. It is preferred to use **docker-desktop**. To change the context refer **step-3**

## Step-3: Navigate to different contexts
```
docker context use <context name>
```
## Step-4: Pull the mongodb community server image.
```
docker pull mongodb/mongodb-community-server:latest
```
## Step-5: Run the container.
```
docker run --name <container name> -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=<user name> -e MONGO_INITDB_ROOT_PASSWORD=<password> -v <dir>:/data/db mongodb/mongodb-community-server
```
note:- If you have any other application running on port 27017 and you are unable to run the container. Refer to **step-6**

## Step-6: Run the container in different port number
```
docker run --name <container name> -d -p <new port number>:27017 -e MONGO_INITDB_ROOT_USERNAME=<user name> -e MONGO_INITDB_ROOT_PASSWORD=<password> -v <dir>:/data/db mongodb/mongodb-community-server
```
## Step-7: Run the Mongosh shell
```
mongosh --port 27017
```
