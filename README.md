docker-symfony
==============

[![Forked from](https://github.com/eko/docker-symfony)

Slightly chaned the setup, removed the ELK container and added Redis.

Just a litle Docker POC in order to have a complete stack for running Symfony into Docker containers using docker-compose tool.

# Installation

First, clone this repository:

```bash
$ git clone git@github.com:eko/docker-symfony.git
```

Next, put your Symfony application into `symfony` folder and do not forget to add `symfony.dev` in your `/etc/hosts` file.

Then, run:

```bash
$ docker-compose up
```

You are done, you can visite your Symfony application on the following URL: `http://symfony.dev`

_Note :_ you can rebuild all Docker images by running:

```bash
$ docker-compose build
```

# How it works?

Here are the `docker-compose` built images:

* `application`: This is the Symfony application code container,
* `db`: This is the MySQL database container (can be changed to postgresql or whatever in `docker-compose.yml` file),
* `php`: This is the PHP-FPM container in which the application volume is mounted,
* `nginx`: This is the Nginx webserver container in which application volume is mounted too,
* `redis`: Redis container e.g. used to store the cache

This results in the following running containers:

```bash
> $ docker-compose ps
        Name                      Command               State              Ports
        -------------------------------------------------------------------------------------------
        jhuitingdockersymfony_application_1   /bin/bash                     Up
        jhuitingdockersymfony_db_1            /entrypoint.sh mysqld         Up      0.0.0.0:3306->3306/tcp
        jhuitingdockersymfony_nginx_1         nginx                         Up      443/tcp, 0.0.0.0:80->80/tcp
        jhuitingdockersymfony_php_1           php5-fpm -F                   Up      9000/tcp
        jhuitingdockersymfony_redis_1         /entrypoint.sh redis-server   Up      0.0.0.0:32768->6379/tcp
```

# Read logs

You can access Nginx and Symfony application logs in the following directories into your host machine:

* `logs/nginx`
* `logs/symfony`
