# tutorial_webapps

- web db server: exment && mariadb latest(10.3.34)
- chat tool: mattermost && postgresql
- monitor tool: zabbix agent


refs: https://exment.net/docs/#/ja/quickstart
refs: https://github.com/exment-git/docker-exment/tree/master/build/php81_mariadb

# install mariadb
refs: https://www.digitalocean.com/community/tutorials/how-to-install-mariadb-on-ubuntu-20-04-ja

# create db
refs: https://exment.net/docs/#/ja/install_mysql?id=mysql%e8%a8%ad%e5%ae%9alinux

```
MariaDB [(none)]> CREATE DATABASE exment_database;
Query OK, 1 row affected (0.000 sec)

MariaDB [(none)]> CREATE USER 'exment_user'@'127.0.0.1' IDENTIFIED BY 'secret';
Query OK, 0 rows affected (0.001 sec)

MariaDB [(none)]> GRANT ALL ON exment_database.* TO exment_user identified by 'secret';
Query OK, 0 rows affected (0.001 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.001 sec)

MariaDB [(none)]> quit
Bye
```



# install php 8.1(see: Dockerfile)
# install fpm, etc(see: Dockerfile)
# install composer(see: Dockerfile)
## update php.ini(see: env/php/php.ini)

# install nginx(see: Dockerfile)
## refs: https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04-ja

## update nginx.conf(see: env/nginx/nginx.conf)
## cp env/nginx/nginx.conf /etc/nginx/conf.d/
## comment out sites-enabled
```
$ diff nginx.conf nginx.conf.bak 
62c62
< 	#include /etc/nginx/sites-enabled/*;
---
> 	include /etc/nginx/sites-enabled/*;
```

## refs nginx php settings https://mat0401.info/blog/ubuntu-nginx-php/

# install exment
