FROM composer:latest as composer
FROM php:8-fpm

RUN docker-php-ext-install pdo_mysql

RUN pecl install apcu

RUN apt-get update && apt-get install -y \
libzip-dev zip libicu-dev

RUN docker-php-ext-install zip intl opcache
RUN docker-php-ext-enable apcu

WORKDIR /var/www/app

COPY --chown=1000:1000 app /var/www/app

RUN PATH=$PATH:/usr/src/app/vendor/bin:bin

RUN composer install --no-scripts --prefer-dist \
  && rm -rf "$(composer config cache-dir)" "$(composer config data-dir)"