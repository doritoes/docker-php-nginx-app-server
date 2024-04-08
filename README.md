# Docker PHP-FPM 8.3 & Nginx 1.24 on Alpine Linux with PDO Support
Implements PHP-FPM 8.3 & Nginx 1.24 container image built on [Alpine Linux](https://www.alpinelinux.org/), with PDO support enabled.

Repository: [https://github.com/doritoes/docker-php-nginx-app-server]
* Built on the lightweight and secure Alpine Linux distribution
* Forked fom best practice repository [https://github.com/TrafeX/docker-php-nginx]

The entire purpose of this repository is to enable PDO support.

⚠️ Currently the console logs this error:
~~~
NOTICE: PHP message: PHP Warning:  PHP Startup: Unable to load dynamic library 'pdo_mysql' (tried: /usr/lib/php83/modules/pdo_mysql (Error loading shared library /usr/lib/php83/modules/pdo_mysql: No such file or directory), /usr/lib/php83/modules/pdo_mysql.so (Error relocating /usr/lib/php83/modules/pdo_mysql.so: pdo_throw_exception: symbol not found)) in Unknown on line 0
~~~

It is uncertain if this is an error trying to relocate the PDO driver, or if the PDO driver will fail. This need to be tested.

[![Docker Pulls](https://img.shields.io/docker/pulls/doritoes/php-nginx-app-server.svg)](https://hub.docker.com/r/doritoes/php-nginx-app-server/)
![nginx 1.24](https://img.shields.io/badge/nginx-1.24-brightgreen.svg)
![php 8.3](https://img.shields.io/badge/php-8.3-brightgreen.svg)
![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)

## Goal of this project
The goal of this container image is to provide an a LAMP application server for use with PDO and an external MySQL service under Kubernetes.

## Usage
Start the Docker container:

    docker run -p 80:8080 doritoes/php-nginx-app-server

See the PHP info on http://localhost, or the static html page on http://localhost/test.html

Or mount your own code to be served by PHP-FPM & Nginx

    docker run -p 80:8080 -v ~/my-codebase:/var/www/html doritoes/php-nginx

## Configuration
In [config/](config/) you'll find the default configuration files for Nginx, PHP and PHP-FPM.
If you want to extend or customize that you can do so by mounting a configuration file in the correct folder;

Nginx configuration:

    docker run -v "`pwd`/nginx-server.conf:/etc/nginx/conf.d/server.conf" doritoes/php-nginx-app-server

PHP configuration:

    docker run -v "`pwd`/php-setting.ini:/etc/php83/conf.d/settings.ini" doritoes/php-nginx-app-server

PHP-FPM configuration:

    docker run -v "`pwd`/php-fpm-settings.conf:/etc/php83/php-fpm.d/server.conf" doritoes/php-nginx-app-server

_Note; Because `-v` requires an absolute path I've added `pwd` in the example to return the absolute path to the current directory_

## Documentation and examples
To modify this container to your specific needs please see the following examples;
* [Adding xdebug support](https://github.com/TrafeX/docker-php-nginx/blob/master/docs/xdebug-support.md)
* [Adding composer](https://github.com/TrafeX/docker-php-nginx/blob/master/docs/composer-support.md)
* [Getting the real IP of the client behind a load balancer](https://github.com/TrafeX/docker-php-nginx/blob/master/docs/real-ip-behind-loadbalancer.md)
* [Sending e-mails](https://github.com/TrafeX/docker-php-nginx/blob/master/docs/sending-emails.md)
