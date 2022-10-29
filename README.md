# Lara-X: Developing with Docker is easy!

<p align="center">
<img src="https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat" alt="contributions welcome">
<a href="https://raw.githubusercontent.com/Yota-X/Lara-X/master/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="GitHub license"></a>
</p>

Lara-X - Laravel development environment based on Docker aimed at facilitating work with Laravel + Docker.

## Installation

 - ```git clone https://github.com/Yota-X/Lara-X.git```
 - ```cd Lara-X```
 - set the values of variables in the .env file
 - copy source code your site to ```app/``` folder
 - ```docker-compose up -d```
 - Enjoy ;)

## Services list:

 - Nginx
 - Mariadb
 - Redis
 - Memcached
 - Supervisor
 - Adminer

## Folder hierarchy

```
├───app                        # Site directory (you must upload your site here)
├───logs                       # Creating after installation. You can save your log files to this folder, for example NGINX logs, you just need to create a volume in the docker-compose.yml file that looks into the ``logs/..`` folder on the host and the folder where the logs are stored in the Docker container
├───nginx                      # Direcory with NGINX config & Dockerfile
│   └───config                 # nginx.conf here
│       └───sites-enabled      # NGINX site config here
├───php-fpm                    # Direcory with PHP-FPM config & Dockerfile
│   └───config                 # php.ini here
└───supervisor                 # Direcory with Supervisor config & Dockerfile
    └───conf.d                 # Supervisor task directory
```

## Docker .env file

```
PROJECT_NAME=Lara-X            # This name will be added to the service name for example Lara-X-redis

ADMINER_PORT=8080              # Adminer port

PHP_VERSION=7.4                # PHP version
PHP_FPM_PORT=9000              # PHP-FPM port

MEMCACHED_PORT=11211           # Memcached port
MEMCACHED_VERSION=1.6          # Memcached version

NGINX_VERSION=1.22.0           # Nginx version
NGINX_HTTP_PORT=80             # Nginx HTTP port
NGINX_HTTPS_PORT=443           # Nginx HTTPS port

MARIADB_VERSION=10.7           # Mariadb version
MARIADB_ROOT_PASSWORD=default  # DB root password
MARIADB_USER=default           # DB user
MARIADB_PASSWORD=default       # DB user password
MARIADB_DATABASE=default       # DB name
MARIADB_PORT=3306              # DB port

REDIS_VERSION=6.2              # Redis version
REDIS_PORT=6379                # Redis port
REDIS_PASSWORD=default         # Redis passowrd

RESTART_MODE=always            # Docker container restart mode
```

## Run Supervisor Task

### Task config example: 

```
[program:Lara-X]
process_name=%(program_name)s_%(process_num)02d
command=/bin/sh -c  "while [ true ]; do (php /var/www/html/artisan schedule:run --verbose --no-interaction &); sleep 60; done"
autostart=true
autorestart=true
numprocs=1
user=www
redirect_stderr=true
```

You can add a file with the ending .conf to the directory ```supervisor/conf.d/``` . Each time you add a new file, restart the Docker container from Supervisor:
```docker-compose restart <PORJECT_NAME_FROM_ENV>-supervisor```

## PHP configuration

You can configure PHP through php.ini file, it is located here ```php-fpm/config/php.ini```

## License

MIT
**Yota-X Free Software, Stand Out!**