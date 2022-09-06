FROM mariadb:10.4 as tutorial-webapps

ARG DEBIAN_FRONTEND=noninteractive

#############################
# web db server: exment && mariadb latest(10.3.34)
# chat tool: mattermost && postgresql
# monitor tool: zabbix agent
#############################


RUN apt update 
#	&& apt -y install curl \
#	&& apt -y install wget \
#	&& apt -y install lsb-release \
#	&& apt -y install gnupg

## web db server

#install mariadb
#RUN apt install -y mariadb-server

#install php 8.1
#refs https://cloudcone.com/docs/article/how-to-install-php-8-1-on-ubuntu-20-04-22-04/
RUN apt install -y ca-certificates apt-transport-https software-properties-common
RUN add-apt-repository ppa:ondrej/php
RUN apt update
RUN apt install -y php8.1

#install fpm, etc
RUN apt update
RUN apt install -y php-fpm
RUN apt install -y git wget gnupg vim unzip libxml2-dev libpng-dev libzip-dev libonig-dev
RUN apt install -y php8.1-gd php8.1-dom php8.1-bcmath php8.1-mbstring php8.1-xml php8.1-zip php8.1-curl
RUN apt install -y  zip unzip

# install composer
RUN apt install -y curl
# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


# install exment
ARG LARAVEL_VERSION="9.*"
ARG EXMENT_VERSION="~5.0"

RUN mkdir /var/www/exment
WORKDIR /var/www/exment
RUN COMPOSER_MEMORY_LIMIT=-1 composer create-project laravel/laravel=${LARAVEL_VERSION} .
RUN composer config --no-plugins allow-plugins.kylekatarnls/update-helper true
RUN composer require psr/simple-cache=^2.0
RUN COMPOSER_MEMORY_LIMIT=-1 composer require exceedone/exment=${EXMENT_VERSION}

RUN php artisan vendor:publish --provider="Exceedone\\Exment\\ExmentServiceProvider"
RUN chown -R www-data:www-data /var/www/exment \
  && chmod 755 -R /var/www/exment/storage \
  && chmod 755 -R /var/www/exment/bootstrap/cache

RUN rm /var/www/exment/.env


ENV EXMENT_DOCKER_MYSQL_PORT 3307
ENV EXMENT_DOCKER_MYSQL_DATABASE exment_database
ENV EXMENT_DOCKER_MYSQL_ROOT_PASSWORD secret
ENV EXMENT_DOCKER_MYSQL_USER exment_user
ENV EXMENT_DOCKER_MYSQL_PASSWORD secret

ENV MYSQL_TCP_PORT=3307
ENV MYSQL_DATABASE exment_database
ENV MYSQL_ROOT_PASSWORD secret
ENV MYSQL_USER exment_user
ENV MYSQL_PASSWORD secret
#install nginx


