
### Docker Communication

https://juejin.cn/post/6844903847383547911

### docker compose example
```yml
#docker network create -d bridge --subnet 192.168.1.0/24 --gateway 192.168.1.1 dockernet
version: "3"
services:
  mysql:
    container_name: mysql
    image: hub.byted.org/task/effect_task_mysql:c9794ba5e600aafcd0b085e351757ef2
    volumes:
      - ../mysql/init_data:/docker-entrypoint-initdb.d
      - ../mysql/temai.cnf:/etc/mysql/conf.d/temai.cnf
    environment:
      MYSQL_DATABASE: ecom_task_test
      MYSQL_ROOT_PASSWORD: root
    restart: always
    ports:
      - 3306:3306
    command: --sql-mode=""
  redis:
    container_name: redis
    image: hub.byted.org/ee/redis:6.0-rc4
    restart: always
    ports:
      - 6379:6379
  es:
    container_name: es
    image: hub.byted.org/ee/elasticsearch:6.5.1
    restart: always
    environment:
      - cluster.name=docker-cluster
      - bootstrap.memory_lock=true
      - discovery.type=single-node
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ports:
      - 9200:9200
  mongo:
    container_name: mongo
    image: hub.byted.org/ee/mongo:4.0.7-xenial
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example
    ports:
      - 27017:27017

```


### Docker vs Docker Compose
The docker cli is used when managing individual containers on a docker engine. It is the client command line to access the docker daemon api.

The docker-compose cli can be used to manage a multi-container application. It also moves many of the options you would enter on the docker run cli into the docker-compose.yml file for easier reuse. It works as a front end "script" on top of the same docker api used by docker, so you can do everything docker-compose does with docker commands and a lot of shell scripting. See this documentation on docker-compose for more details.


### Docker Compose vs K8s
Docker Compose is designed to run containers on a single host system. In contrast, Kubernetes can manage containers deployed across multiple nodes(computers).