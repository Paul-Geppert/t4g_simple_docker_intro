# Simple Mongo and Mongo-Express Example

[![Alt text](https://tech.4germany.org/wp-content/uploads/2020/01/Logo-Final-02-copy-1-300x109-1.png)](https://tech.4germany.org)

Find more information about Docker networking at [https://docs.docker.com/network](https://docs.docker.com/network).

Find more information about `mongo` and `mongo-express` in Docker at [https://hub.docker.com/_/mongo](https://hub.docker.com/_/mongo) and [https://hub.docker.com/_/mongo-express](https://hub.docker.com/_/mongo-express).

## Variant 1 - Docker

### Variant 1.1

Use the host network stack. `localhost` in Containers will point to the host machine.

Find the network visualization below.

```sh
Network visualization of variant 1.1

+-----------+        +-----------------+
|           |        |                 |
|   Mongo   |        |  Mongo-Express  |
|           |        |                 |
+-----o-----+        +--------o--------+
      |                       |
      | Shared Port 27017     | Shared Port 8081
      |                       |
+-----o-----------------------o--------+
|                                      |
|                Host                  |
|                                      |
+--------------------------------------+
```

### How to execute 1.1

```sh
docker volume create t4g_mongo_vol

docker run --rm -d \
--name t4g_mongo \
-v t4g_mongo_vol:/data/db \
--network host \
-e MONGO_INITDB_ROOT_USERNAME=root \
-e MONGO_INITDB_ROOT_PASSWORD=example \
mongo

docker run --rm -d \
--name t4g_mongo_express \
--network host \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=root \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=example \
# use 'localhost' as we use host network
-e ME_CONFIG_MONGODB_URL=mongodb://root:example@localhost:27017/ \
mongo-express
```

### Variant 1.2

Explicitely create a network to connect the containers. This gives more control, e.g. over exposed ports.

Find the network visualization below.

```sh
Network visualization of variant 1.2

+-----------+        +-----------------+
|           |        |                 |
|   Mongo   o--------o  Mongo-Express  |
|           |        |                 |
+-----------+        +--------o--------+
                              | Container-Port 8081
                              |
                              | Host-Port 8081
+-----------------------------o--------+
|                                      |
|                Host                  |
|                                      |
+--------------------------------------+
```

### How to execute 1.2

```sh
docker volume create t4g_mongo_vol

docker network create t4g_mongo_net

docker run --rm -d \
--name t4g_mongo \
-v t4g_mongo_vol:/data/db \
--network t4g_mongo_net \
-e MONGO_INITDB_ROOT_USERNAME=root \
-e MONGO_INITDB_ROOT_PASSWORD=example \
mongo

docker run --rm -d \
--name t4g_mongo_express \
--network t4g_mongo_net \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=root \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=example \
# you can reference other containers by their name when using docker networks
-e ME_CONFIG_MONGODB_URL=mongodb://root:example@t4g_mongo:27017/ \
-p 8081:8081 \
mongo-express
```

### Cleanup

```sh
docker stop t4g_mongo_express
docker stop t4g_mongo
docker volume rm t4g_mongo_vol
# For 1.2 also remove the network
docker network rm t4g_mongo_net
```

## Variant 2 - Docker Compose

### How to execute

1. Start the containers: `docker-compose up -d`
2. Access [http://127.0.0.1:8090](http://127.0.0.1:8090) to test the app.
3. Stop the container: `docker-compose down` or `docker-compose down -v` to remove the volume too
