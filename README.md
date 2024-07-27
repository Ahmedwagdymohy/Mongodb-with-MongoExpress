# How to start MongoDB with Mongo Express using Docker
## 1- Using Command Line:
-   Download Docker and Docker-compose 
-   Download MongoDB Image from [here](https://hub.docker.com/_/mongo) 
-   Download MongoExpress Image from [here](https://hub.docker.com/_/mongo-express)
-   or Use commands directly :
```bash
docker pull mongo
docker pull mongo-express
```
-   Now we have the images installed You can verify by writing:
```bash
docker images
```
- You will see all the Images you have listed
- Let's create a network bridge so the two images can see each others:
```bash
docker network create NETWORKNAME
```
- Let's start creating 2 Containers for each image :
> [!WARNING]
> Don't forget to change the network name in the command below

```bash
docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=pass --name mongo --network mongo-network mongo
```
- To check the Two containers are running use:
```bash
docker ps
```

- Now you can connect to the UI of MongoExpress uing 
`localhost:8081`



## 2- Using Docker-Compse:
- create a `Docker-compose.yml` file and use the following code :
```yml
version: '3.8'
services:
  mongodb:
    image: mongo:latest # use the latest image.
    container_name: mongodb
    restart: unless-stopped
    environment: # set required env variables to access mongo
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: password
    ports:
      - 27017:27017
    volumes: # optional to preserve database after container is deleted.
      - ./database-data:/data/db
  
  # Mongo Express Service
  mongo-express:
    image: mongo-express:latest # latest image
    container_name: mongo-express
    restart: unless-stopped
    ports:
      - 8081:8081
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: root
      ME_CONFIG_MONGODB_ADMINPASSWORD: password
      ME_CONFIG_MONGODB_SERVER: mongodb 
      # use the name of the mongo container above for server env var.
      # In our case this is mongodb
```
-   save and exit
```bash
docker-compose up -d
```
- It will show:
- ![Screenshot from 2024-07-25 19-05-46](https://github.com/user-attachments/assets/a25dce2a-1042-400c-a0c2-a6277e04b04e)




- Now you can connect to the UI of MongoExpress uing 
`localhost:8081`


# Attatchment:
![image](https://github.com/user-attachments/assets/b3a2a491-6d1d-435c-ac55-425ffbc3dee6)
![image](https://github.com/user-attachments/assets/36f26a29-72b5-4cec-8948-1e9417e8400d)


