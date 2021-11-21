# PHP-FPM Docker Images

Docker container to install and run [PHP-FPM](https://php-fpm.org/).

## Project Goal

Out of the box, fully loaded PHP-FPM docker images, that can support all my PHP projects. I work with Yii2 & Laravel.
The images are no light weight.

## Dockerfile links

-   [Dockerfile](https://github.com/docker-official/nginx-php-fpm/blob/main/Dockerfile/php-fpm/Dockerfile)

## Installed extensions

- amqp
- bcmath
- Core
- ctype
- curl
- date
- dom
- fileinfo
- filter
- ftp
- gd
- gettext
- gmp
- hash
- iconv
- intl
- json
- libxml
- mbstring
- mcrypt
- mongodb
- mysqli
- mysqlnd
- openssl
- pcntl
- pcre
- PDO
- pdo_mysql
- pdo_pgsql
- pdo_sqlite
- Phar
- posix
- readline
- redis
- Reflection
- session
- shmop
- SimpleXML
- soap
- sockets
- SPL
- sqlite3
- standard
- swoole
- sysvmsg
- sysvsem
- sysvshm
- tokenizer
- xhprof
- xml
- xmlreader
- xmlrpc
- xmlwriter
- Zend OPcache
- zip
- zlib

## Installed Zend Modules

-   Zend OPcache

## Pull latest image

```sh
docker pull classes/php:7.1-fpm-v1.0.1
```

## Running PHP apps

### Running image

Run the PHP-FPM image, mounting a directory from your host.

```sh
docker run -it --name php-fpm -v /path/to/your/app/www:/var/www/html classes/php:7.1-fpm-v1.0.1
```

or using [Docker Compose](https://docs.docker.com/compose/):

```sh
version: '3'
services:
  php-fpm:
    container_name: php-fpm
    image: classes/php:7.1-fpm-v1.0.1
    volumes:
      - "/path/to/your/app/www:/var/www/html"
```

### Running as server

```sh
docker run -d --name php-fpm -v /path/to/your/app/www:/var/www/html classes/php:7.1-fpm-v1.0.1
```

### Logging

```sh
docker logs php-fpm
```

# Listing installed extensions

```sh
docker run --rm -it classes/php:7.1-fpm-v1.0.1 php -m
```

