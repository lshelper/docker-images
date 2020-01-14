FROM php:7.3-fpm

RUN apt-get update

RUN apt-get install -y \
    curl \
    wget \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libzip-dev
RUN  docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd


RUN pecl install mcrypt-1.0.2 && docker-php-ext-enable mcrypt

RUN apt-get install -y \
    libxml2-dev
RUN docker-php-ext-install soap && docker-php-ext-enable soap

RUN apt-get install -y libmagickwand-6.q16-dev --no-install-recommends \
    && ln -s /usr/lib/x86_64-linux-gnu/ImageMagick-6.8.9/bin-Q16/MagickWand-config /usr/bin \
    && pecl install imagick \
    && echo "extension=imagick.so" > /usr/local/etc/php/conf.d/ext-imagick.ini

RUN docker-php-ext-install opcache && docker-php-ext-enable opcache

