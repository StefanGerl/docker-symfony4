FROM php:7.3.6-fpm

RUN docker-php-ext-install pdo_mysql

RUN pecl install apcu
RUN docker-php-ext-enable apcu

RUN apt-get update
RUN apt-get install -y git zip unzip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && mv composer /usr/local/bin/composer

WORKDIR /usr/src/app

RUN PATH=$PATH:/usr/src/apps/vendor/bin:bin
