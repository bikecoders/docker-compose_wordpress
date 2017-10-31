# Dev environment WordPress with Docker _**TIPS**_

#### This docker compose was made to have a modern WP dev environment which can be portable, easy to set up and focused on the use of `wp`.

> With `docker-compose up` it will run a phpmyadmin service, this is created with goal of facilitate the management of the DataBase (not all of us are command ninja) so we recommend, stop it when you are not using it.
> `docker-compose stop wp_phpmyadmin`

## Start everything

For be able to manipulate easily the files of wordpress you need to:

`export UID && docker-compose up`

## Steps to begin with a new WP project

1. Create the user using phpmyadmin
    - allow conection from any host
    - create a database with the same name with all priviledges
2. Download the WordPress core using
    - `docker-compose exec wp_server wp core download`
3. Create your `wp-config` file
    - `docker-compose exec wp_server wp core config --prompt`
      - 1/12 --dbname=<**dbname**>: `YOUR_DB_NAME`
      - 2/12 --dbuser=<**dbuser**>: `USER_CREATED_AT_1`
      - 3/12 [--dbpass=<**dbpass**>]: `PASS_CREATED_AT_1`
      - 4/12 [--dbhost=<**dbhost**>]: `wp_mariadb`
      - 5...12 - Default values set by enter
4. Install WordPress site
    - `docker-compose exec wp_server wp core install --prompt`
      - 1/6 --url=<**url**>: `localhost`
      - 2...6 - Your personal configuration

------------------

## Changing the PHP version

1. stop everything with
    - `docker-compose stop`

2. On the `docker-compose.yml` file, on service `wp_server` on the section `args` leave uncommented the php version that you want
    ```yml
        args:
            PHP_VERSION: 7.1
            # PHP_VERSION: 7.0
            # PHP_VERSION: 5.6
    ```
3. Then build the new image with:
    - `docker-compose build`
4. Run everything again:
    - `export UID && docker-compose up`

5. To verify the version run
    - `docker exec wp_server php --version`

------------------

## Deploying your database

We recommend to have a repo for your WordPress site, so the themes and plugins should be deployed by a `git pull` command.

> By the moment we don't expose the wordmove entrypoint in the container so you need to login to container and execute the following commands

### Login in to the container

`docker-compose run --rm  wp_wordmove /bin/bash`

### Deploying `uploads` folder

`wordmove push --uploads`

### Deploying your database

`wordmove push --db`

> #### The database deploy will overwritte the database on the production site, each comment, post, subscriber that is not in your local database will be lost


> Written with [StackEdit](https://stackedit.io/).
