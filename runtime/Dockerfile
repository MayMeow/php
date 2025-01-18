FROM php:8.2.20-fpm-bullseye

# arguments in docker-compose file
ARG PUID=20021
ARG PGID=20021
ARG HOME_DIR="/home/www-data"

# Install Libraries
RUN apt-get update \
    && apt-get install --fix-missing -y unzip libicu-dev libpq-dev zlib1g-dev libpng-dev libzip-dev netcat

# Install PHP Extensions
RUN docker-php-ext-install intl pdo_pgsql gd zip pdo_mysql

# PHP Pecl Redis extensions
RUN pecl install redis
RUN docker-php-ext-enable redis

# Clean
RUN apt autoremove --purge -y \
    && apt clean
    
# Create system user to run Composer and Artisan Commands
# RUN useradd -G www-data,root -u $uid -d /home/$user $user
# RUN mkdir -p /home/$user/.composer && \
#     chown -R $user:$user /home/$user

RUN groupmod -g $PGID www-data && \
    usermod -u $PUID -g $PGID -d $HOME_DIR www-data && \
    mkdir -p $HOME_DIR && \
    chown -R www-data:www-data $HOME_DIR && \
    find / -user 33 -exec chown -h $PUID {} \; && \
    find / -group 33 -exec chgrp -h $PGID {} \;
