#
# Phalcon 4 + PHP 7.3
#

# Pull base image
FROM php:7.3-cli-alpine

MAINTAINER Ruud Boon <ruud@ruudboon.io>

RUN docker-php-ext-install pdo_mysql
RUN apk --update add bash yaml-dev fcgi composer gettext-dev libpng-dev postgresql-dev

RUN \
    apk add --virtual build-dependencies \
        autoconf \
        g++ \
        pcre-dev \
        file \
        re2c \
        make \
    && pecl install psr \
    && docker-php-ext-enable psr \
    && curl -sS -o /tmp/phalcon.tar.gz https://codeload.github.com/phalcon/cphalcon/tar.gz/v4.0.0-alpha.4 \
    && cd /tmp/ \
    && tar xvzf phalcon.tar.gz \
    && cd cphalcon-4.0.0-alpha.4/build \
    && sh install \
    && docker-php-ext-enable phalcon --ini-name z-docker-php-ext-phalcon.ini \
    && pecl install yaml \
    && pecl install redis \
    && pecl install xdebug-2.7.0beta1 \
    && docker-php-ext-enable yaml redis xdebug \
    && docker-php-ext-install gettext \
    && docker-php-ext-enable gettext \
    && docker-php-ext-install gd \
    && docker-php-ext-enable gd \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-enable pdo_pgsql \
    && apk del build-dependencies \
    && rm -rf cphalcon-4.0.0-alpha.4 \
        4.0.x \
        /var/cache/apk/* \
        /tmp/* \
        /var/tmp/*

RUN curl -LsS https://codeception.com/codecept.phar -o /usr/local/bin/codecept
RUN chmod a+x /usr/local/bin/codecept

WORKDIR /project
