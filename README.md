# Dev environment WordPress with Docker _**TIPS**_ 


#### This docker compose was made to have a modern WP dev environment which can be portable, easy to set up and focused on the use of `wp-cli`.

> With `docker-compose up` it will run a phpmyadmin service, this is created with goal of facilitate the management of the DataBase (not all of us are command ninja) so we recommend, stop it when you are not using it.
> `docker-compose stop wp_phpmyadmin`

## Steps to begin with a new WP project

1. Create the user using phpmyadmin
	- Set as `Host name` **=** `Use text field`= `wp_server`
2. Download the WordPress core using `docker exec wp_server wp-cli core download`
3. Create your `wp-config` file `docker exec -ti wp_server wp-cli core config --prompt`
  - 1/12 --dbname=<**dbname**>: `YOUR_DB_NAME`
  - 2/12 --dbuser=<**dbuser**>: `USER_CREATED_AT_1`
  - 3/12 [--dbpass=<**dbpass**>]: `PASS_CREATED_AT_1`
  - 4/12 [--dbhost=<**dbhost**>]: `wp_mariadb`
  - 5...12 - Default values set by enter
4. Create db `docker exec -ti wp_server wp-cli db create`
5. Install WordPress site `docker exec -ti wp_server wp-cli core install --prompt`
  - 1/6 --url=<**url**>: `localhost`
  - 2...6 - Your personal configuration

## DB useful commands
### Log into
`docker exec -ti wp_mariadb mysql -h localhost -u root -pPASSWORD`

### Create db
`docker exec -ti wp_mariadb mysql -h localhost -u root -pPASSWORD`

```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 19
Server version: 10.2.7-MariaDB-10.2.7+maria~jessie mariadb.org binary distribution

Copyright (c) 2000, 2017, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> CREATE DATABASE test CHARACTER SET utf8 COLLATE utf8_bin;

MariaDB [(none)]> SHOW DATABASES;
```

> Written with [StackEdit](https://stackedit.io/).

