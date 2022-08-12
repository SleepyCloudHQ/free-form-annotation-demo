# Setup licence
The easiest way to setup a licence is by mounting a local directory containing the licence as a volume. And then setting the `LICENCE_FILE_PATH` env variable.

Example:

```docker-compose
  backend:
    image: ffat-backend
    restart: always
    volumes:
      - ./licence:/licence
    environment:
      - LICENCE_FILE_PATH=/licence/licence.txt
```
# Setup DB
## Using SQLITE
To use SQLite as your DB, you can simply set the `SQLITE_FILE_PATH` env variable on the backend container. (Use a volume in order to persist the data)

Example:

```docker-compose
  backend:
    image: ffat-backend
    restart: always
    volumes:
      - ./data:/root/data
    environment:
      - SQLITE_FILE_PATH=/root/data/storage.db
```
## Using MySQL
On the other hand, if you want to use a mysql server you can set it up via these env variables: `MYSQL_HOST`, `MYSQL_USER`, `MYSQL_PASS`,  `MYSQL_DBNAME`

Example:

```docker-compose
  backend:
    image: ffat-backend
    restart: always
    environment:
      - MYSQL_HOST=db
      - MYSQL_USER=user
      - MYSQL_PASS=user_pass
      - MYSQL_DBNAME=ffat
  db:
    image: mariadb
    ports:
      - 3306:3306
    volumes:
      - ./db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=root_pass
      - MYSQL_PASSWORD=user_pass
      - MYSQL_USER=user
      - MYSQL_DATABASE=ffat
```

# Run the project
* Run the following command:

```console
$ docker-compose up
```

* Navigate to `http://ffat.localhost/`
* Enjoy

# Run the migrations
Execute the following command:

```console
$ docker exec compose_backend_1 ./migrate
```
where `compose_backend_1` is the container's name

# Creating an user
There are 2 types of users: `admin` and `annotator`. Admins can see/tag all the datasets. Additionally, admins can manage roles and access permissions of the annotators. Created users are annotators by default. To create an admin user include a `-admin` flag

Creating an annotator user:

```console
$ docker exec compose_backend_1 ./create_user -u <email> -p <password>
```

Creating an admin user:

```console
$ docker exec compose_backend_1 ./create_user -u <email> -p <password> -admin
```

# Mouting a data folder
To make importing/exporting easier we can mount a data folder to the backend container

Example:

```docker-compose
  backend:
    image: ffat-backend
    restart: always
    volumes:
      - ./data:/root/data
```

# Importing data
To import data run the following command:

```console
$ docker exec compose_backend_1 ./import_dataset -f data/import_data.json -n "Example dataset" -e entity1, entity2,entity3 -r relationship1,relationship2,relationship3
```

Flags:

* `-f` file path to json file to be imported
* `-n` name of the dataset
* (optional) `-e` list of predefined entity tag options separated by `,`
* (optional) `-r` list of predefined relationship tag options separated by `,`


# Exporting data
To export data run the following command:

```console
$ docker exec compose_backend_1 ./export_dataset -f data/exported_data.json -d 1
```
Flags:

* `-f` file path to location where the data should be exported
* `-d` the ID of the dataset to be exported



