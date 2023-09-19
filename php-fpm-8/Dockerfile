#syntax=docker/dockerfile:1.4
#
# A php-fpm 8 image with composer, sqlite, and the amqp, apcu, intl, opcache, and zip extensions.
#
ARG PHP_VERSION=8.2
ARG COMPOSER_VERSION=2

FROM composer/composer:${COMPOSER_VERSION}-bin AS composer
FROM mlocati/php-extension-installer:latest AS php_extension_installer
FROM php:${PHP_VERSION}-fpm-alpine

# php extensions installer: https://github.com/mlocati/docker-php-extension-installer
COPY --from=php_extension_installer --link /usr/bin/install-php-extensions /usr/local/bin/

RUN apk add --no-cache \
  acl \
  fcgi \
  file \
  gettext \
  sqlite \
  ;

RUN set -eux; \
  install-php-extensions \
  intl \
  zip \
  apcu \
  opcache \
  amqp \
  pcntl \
  pdo \
  pdo_mysql \
  pdo_pgsql \
  ;

RUN mkdir -p /var/run/php

# https://getcomposer.org/doc/03-cli.md#composer-allow-superuser
ENV COMPOSER_ALLOW_SUPERUSER=1
ENV PATH="${PATH}:/root/.composer/vendor/bin"

COPY --from=composer --link /composer /usr/bin/composer
