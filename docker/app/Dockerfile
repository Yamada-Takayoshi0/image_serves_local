FROM php:8.3-apache

ADD php.ini /usr/local/etc/php/
ADD 000-default.conf /etc/apache2/sites-enabled/

COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

# RUN apt update && apt install -y zlib1g-dev g++ libicu-dev zip libzip-dev zip libpq-dev \
#     && docker-php-ext-install intl opcache pdo pgsql pdo_pgsql \
#     && pecl install apcu \
#     && docker-php-ext-enable apcu \
#     && docker-php-ext-configure zip \
#     && docker-php-ext-install zip \
#     && apt-get install -y git \
#     && a2enmod rewrite 

RUN apt-get update \
    && apt-get install -y \
    git \
    zip \
    unzip \
    vim \
    libzip-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libpq-dev \
    ghostscript \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo_mysql zip

RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -\
    && apt-get install -y nodejs

RUN mv /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled
RUN /bin/sh -c a2enmod rewrite

WORKDIR /var/www/html