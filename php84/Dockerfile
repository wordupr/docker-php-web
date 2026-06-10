FROM php:8.4-fpm

LABEL maintainer="pi@wordupr.com"

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    libcurl4-openssl-dev \
    libgmp-dev \
    libonig-dev \
    libyaml-dev \
    libsodium-dev \
    libicu-dev \
    libz-dev \
    libpq-dev \
    libzip-dev \
    libonig-dev \
    libjpeg62-turbo-dev \
    libjpeg-dev \
    libpng-dev \
    libwebp-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
    zlib1g-dev \
    libxml2-dev \
    libbz2-dev \
  && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-configure mbstring --enable-mbstring \
    && docker-php-ext-configure soap --enable-soap \
    && docker-php-ext-configure exif --enable-exif \
    && docker-php-ext-install \
        bcmath \
        intl \
        mbstring \
        mysqli \
        pcntl \
        pdo_mysql \
        sockets \
        zip \
        soap \
        exif \
        curl \
        fileinfo \
        gmp \
        xml \
  && docker-php-ext-install opcache \
  && docker-php-ext-enable opcache


RUN docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype \
            && docker-php-ext-install gd; 

RUN pecl install -o -f redis && docker-php-ext-enable redis;

RUN pecl install -o -f protobuf  && docker-php-ext-enable protobuf;

RUN pecl install -o -f yaml && docker-php-ext-enable yaml;

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

WORKDIR /var/www