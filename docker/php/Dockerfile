FROM php:fpm

COPY php.ini /usr/local/etc/php/conf.d/docker-php-config.ini

RUN apt-get update && apt-get install -y \
    gnupg \
    g++ \
    procps \
    openssl \
    git \
    unzip \
    zlib1g-dev \
    libzip-dev \
    libpng-dev \
    libjpeg-dev \
    libicu-dev  \
    libonig-dev \
    libxslt1-dev \
    libfreetype6-dev \
    acl \
    sudo \
    iputils-ping

RUN mkdir /conf.d

RUN docker-php-ext-install gd

# RUN docker-php-ext-configure gd --with-jpeg --with-freetype

RUN docker-php-ext-install \
    pdo pdo_mysql zip xsl opcache exif mbstring

# Configure non-root user.

RUN groupadd -g 1001 develop
RUN useradd -g develop develop
RUN usermod -aG sudo develop

# Source code
RUN chown develop:develop /var/www
RUN chown -R develop:develop /conf.d

RUN mkdir /home/develop
RUN chown -R develop:develop /home/develop
# COPY --chown=develop:develop ./ /var/www

# root and develop passwords 123
RUN usermod -p $(openssl passwd -6 '123') root
RUN usermod -p $(openssl passwd -6 '123') develop

WORKDIR /var/www

# Composer
# COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

USER develop

# CMD php

EXPOSE 9000