# Docker

Environment for PHP developer.  

## Commands

List containers:

```docker ps -as```

Remove container:

```docker rm my_container_name```

List images:

```docker images```

Remove image:

```docker rmi my_image_name```

Run composer:

```docker-compose exec --user www-data mycontainer composer install```

Start docker: (be in folder)

```docker-compose up -d```

Start all containers:

```docker restart $(docker ps -q)```

Stop all containers:

```docker stop $(docker ps -a -q)```

Check CPU consumption:

```docker stats $(docker inspect -f "{{ .Name }}" $(docker ps -q))```

Delete all containers:

```docker rm $(docker ps -aq)```

Delete all images:

```docker rmi $(docker images -q)```

Docker rebuild: (be in folder) 

```docker-compose up -d --build```

Dockers stop: (be in folder)

```docker-compose kill``` 

## Structure

* docker/
    * nginx/ - container name
        * Dockerfile - container configuration
        * default.conf - nginx configuration to override 
    * php-fpm/
        * php7.0/
            * Dockerfile
* RoboFile.php
* docker-compose.yml
* robo

## docker-compose.yml


```
version: "2.0"

services:
    nginx:
        build: 'docker/nginx'
        container_name: my-nginx
        links:
            - 'php-fpm'
        ports:
            - '8088:80'
        restart: 'always'
        volumes_from:
            - 'php-fpm'
            
    php-fpm:
        build: 'docker/php-fpm'
        container_name: my-php
        ports:
            - "9000:9000"
        volumes:
            - './www/:/var/www/'
        links:
            - postgres
        working_dir: /var/www
        
    postgres:
        image: postgres
        container_name: my-postgres
        volumes:
            - ./www/:/var/www/
        ports:
            - "5433:5432"
```

Service ( e.g. nginx ) have a key `build` or `image`.

1. build - we have extra configuration in `docker/nginx/Dockerfile`
2. image - download image from docker repository

## Dockerfile

e.g.  /docker/nginx/Dockerfile

```
FROM nginx:latest

COPY default.conf /etc/nginx/conf.d/default.conf
```

1. FROM - download image from docker repository
2. COPY - copy configuration
