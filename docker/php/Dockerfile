FROM php:8.2-fpm

# System dependencies install karein
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip

# PHP extensions install karein
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Composer install karein
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html
