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
> [!NOTE]
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
