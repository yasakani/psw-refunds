FROM php:7.1-apache-stretch

ARG DEBIAN_FRONTEND=noninteractive

# working directory
WORKDIR /app

# system dependencies
RUN apt-get update \
    && apt-get install -qq --yes --no-install-recommends \
    apt-utils \
    ca-certificates \
    libxml2-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libxpm-dev \
    libwebp-dev \
    libcurl4-openssl-dev \
    libzip-dev \
    file \
    g++ \
    make \
    uuid-runtime \
    git \
    zip \
    unzip \
    && apt-get autoremove \
    && apt-get clean \
    && apt-get autoclean

# php extensions
RUN apt-get update && apt-get install -y libmcrypt-dev \
    && pecl install mcrypt-1.0.2 \
    && docker-php-ext-enable mcrypt

RUN docker-php-ext-install gd \
    && docker-php-ext-enable gd

RUN docker-php-ext-install pdo_mysql \
    && docker-php-ext-enable pdo_mysql

RUN apt-get update && apt-get install -y zlib1g-dev \
    && docker-php-ext-install zip

RUN docker-php-ext-install exif pcntl

# xdebug (for development purposes)
RUN pecl install xdebug-2.7.2 \
    && docker-php-ext-enable xdebug
COPY php/xdebug.ini /usr/local/etc/php/conf.d/xdebug-dev.ini

# composer
ENV COMPOSER_ALLOW_SUPERUSER=1
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# apache config
RUN a2enmod rewrite
ENV APACHE_DOCUMENT_ROOT /app/public
ADD apache/000-default.conf /etc/apache2/sites-available/
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
RUN sed -i '$ a\ServerName localhost' /etc/apache2/apache2.conf

# ports
EXPOSE 80

# command
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
