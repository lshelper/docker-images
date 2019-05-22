FROM php:5.6-fpm

RUN apt-get update
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libz-dev zlib1g-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN apt-get install -y \
  curl \
  wget \
  git \
  libxslt-dev \
  libicu-dev \
  libmcrypt-dev \
  libpng-dev \
  libxml2-dev \
  && docker-php-ext-install -j$(nproc) mcrypt mbstring mysqli pdo_mysql zip \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-configure intl
RUN docker-php-ext-install -j$(nproc)  intl
RUN docker-php-ext-install -j$(nproc)  xsl
RUN docker-php-ext-install -j$(nproc)  soap

RUN apt-get install -y \
  libmagickwand-dev --no-install-recommends \
  && pecl install imagick \
  && docker-php-ext-enable imagick