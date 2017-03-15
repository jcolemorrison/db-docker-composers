# Docker Compose Files for MySQL and mongoDb

A docker compose file to setup both a MySQL and MongoDB docker container.

## Simple Usage

1) Go to any project directory

2) Insert the `docker-compose.yml` file

3) Run `docker-compose up -d` in the directory with the file

4) Run `docker-compose logs -f` to see what's happening in the DB

5) Run `docker-compose down` to cleanup the containers when no longer needed

_all docker-compose commands must be run in the directory with the docker-compose file_

Below are specific to which compose you are using.

### MySQL

You can edit the environment variables in the `docker-compose.yml` file to your liking.  They become the root and non-root user credentials.  To connect to the MySQL instance client:

```bash
$ docker-compose exec mysqlDb mysql -u devuser -p
```

for the regular user

and

```bash
$ docker-compose exec mysqlDb mysql -p
```

for the root user.

You'll be prompted for the passwords which are also defined in the `docker-compose.yml` environment variables section.

### MongoDB

Remove the `command: mongod --auth` if you do not want to deal with authentication and separate users.

To get this up and running with an admin user:

1) Connect to the one time login to create our admin user:

```bash
$ docker-compose exec mongoDb mongo
```

2) Switch to the Admin DB and Create a Root user:

```bash
use admin
```

and then

```js
db.createUser(
  {
    user: "devadmin",
    pwd: "devadmin",
    roles: [ { role: "root", db: "admin" } ]
  }
)
```

3) Exit the Mongo console.

Now in order to do anything to the MongoDB instance's collections, databases, etc. you must authenticate when logging in:

```bash
$ docker-compose exec mongoDb mongo -u devadmin -p devadmin --authenticationDatabase "admin"
```

For more information see the full article:

## [Docker for a Fresh MySQL or MongoDB Instance in Any Project](http://start.jcolemorrison.com/docker-with-mysql-or-mongodb-instances-in-projects)






