FROM php:8.3.16-fpm-bookworm

# Install Libraries
RUN apt-get update \
    && apt-get install --fix-missing -y unzip libicu-dev libpq-dev zlib1g-dev libpng-dev libzip-dev netcat-traditional

# Install PHP Extensions
RUN docker-php-ext-install intl pdo_pgsql gd zip pdo_mysql

# PHP Pecl Redis extensions
RUN pecl install redis
RUN docker-php-ext-enable redis

# Clean
RUN apt autoremove --purge -y \
    && apt clean
