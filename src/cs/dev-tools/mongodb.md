# MongoDB basic

### How to install MongoDB on Ubuntu 20.04

```shell
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
sudo apt update
sudo apt-get install gnupg
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

### How to start MongoDB

```shell
sudo systemctl start mongod
```

### How to operate MongoDB

* Show databases

```mongodb
show dbs
```

* Choose database

```mongodb
use <DATABASE_NAME>
```

* Get current databse

```mongodb
db
```

* Delete databse

```mongodb
db.dropDatabase()
```

* Show collections:

```mongodb
show collections
# or
db.getCollectionNames()
```

* delete collection

```mongodb
db.<collection_name>.drop()
```

* select \* from xxxx:

```mongodb
db.<collection_name>.find()
# or with more options
db.<collection_name>.find(query, projection).pretty()
```

### References

[https://www.runoob.com/mongodb/mongodb-dropdatabase.html](https://www.runoob.com/mongodb/mongodb-dropdatabase.html)

[https://computingforgeeks.com/how-to-install-mongodb-database-on-ubuntu/](https://computingforgeeks.com/how-to-install-mongodb-database-on-ubuntu/)
