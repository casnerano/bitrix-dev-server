FROM composer:latest AS composer_builder
FROM php:8.2-fpm

RUN apt-get update && apt-get install -y --no-install-recommends \
    libpng-dev \
    libjpeg62-turbo-dev \
    libxpm-dev \
    libwebp-dev \
    libfreetype6-dev \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    libmcrypt-dev

RUN docker-php-ext-configure gd \
    --with-jpeg \
    --with-xpm \
    --with-freetype \
    --with-webp

RUN docker-php-ext-install \
    bcmath \
    calendar \
    exif \
    gettext \
    mysqli \
    sockets \
    opcache \
    gd \
    soap \
    zip

COPY --from=composer_builder "/usr/bin/composer" "/usr/bin/composer"

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

COPY "./conf.d/custom.ini" "$PHP_INI_DIR/conf.d/custom.ini"

WORKDIR /var/www