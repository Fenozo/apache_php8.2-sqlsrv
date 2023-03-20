FROM php:8.2-apache


RUN apt-get update \
&& apt-get install -y curl git unzip libpq-dev libicu-dev libzip-dev gnupg \
zlib1g-dev g++ libpng-dev libonig-dev unixodbc-dev \
&& curl -s https://getcomposer.org/installer > composer_installer.php && \ 
php composer_installer.php \
&& mv composer.phar /usr/local/bin/composer && \
rm composer_installer.php



RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/prod.list > /etc/apt/sources.list.d/mssql-release.list

RUN apt-get install -y msodbcsql18 && mssql-tools18


RUN apt-get update && \
    docker-php-ext-install mysqli pdo pdo_mysql

RUN pecl install sqlsrv-5.11.0beta1
RUN pecl install pdo_sqlsrv-5.11.0beta1

EXPOSE 80

WORKDIR /var/www/html