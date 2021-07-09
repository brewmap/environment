FROM php:8.0.8-fpm-alpine

ARG COMPOSER_VERSION
ENV COMPOSER_HOME=/application/.composer
ENV COMPOSER_MEMORY_LIMIT=-1

RUN apk update && apk upgrade \
    && apk add --no-cache php8-pear php8-dev icu-dev \
    && apk add --no-cache --virtual .build-deps gcc musl-dev make \
    && curl -sS https://getcomposer.org/installer | php -- --version=${COMPOSER_VERSION} --install-dir=/usr/local/bin --filename=composer \
    && docker-php-ext-configure intl \
    && docker-php-ext-install mysqli pdo pdo_mysql intl \
    && docker-php-ext-enable intl \
    && pecl install -o -f redis \
    && docker-php-ext-enable redis \
    && apk del .build-deps
