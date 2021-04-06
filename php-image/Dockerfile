FROM php:7.4.16-fpm-alpine3.13

LABEL maintainer="Oleg Cvetkov <ovc@digit-it.ru>"

RUN apk add --update --no-cache \
  freetype-dev \
  libjpeg-turbo-dev \
  libpng-dev \
  icu-dev \
  openldap-dev \
  libxml2-dev \
  libzip-dev \
  bzip2-dev \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) \
    gd \
    mysqli \
    intl \
    ldap \
    xmlrpc  \
    exif \
    zip \
    bz2 \
    opcache

RUN apk add --update --no-cache --virtual .build-dependencies $PHPIZE_DEPS \
  && pecl install apcu \
  && docker-php-ext-enable apcu \
  && pecl clear-cache \
  && apk del .build-dependencies