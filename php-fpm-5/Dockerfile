#syntax=docker/dockerfile:1.4
#
# A legacy php-fpm 5 image with composer.
#
ARG PHP_VERSION=5.6
ARG COMPOSER_VERSION=2.2

FROM composer/composer:${COMPOSER_VERSION}-bin AS composer
FROM php:${PHP_VERSION}-fpm-alpine

RUN apk add --no-cache \
  acl \
  fcgi \
  file \
  ;

RUN mkdir -p /var/run/php

# https://getcomposer.org/doc/03-cli.md#composer-allow-superuser
ENV COMPOSER_ALLOW_SUPERUSER=1
ENV PATH="${PATH}:/root/.composer/vendor/bin"

COPY --from=composer --link /composer /usr/bin/composer
