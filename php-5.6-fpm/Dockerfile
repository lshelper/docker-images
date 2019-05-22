FROM php:5.6-fpm

RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        curl \
        wget \
        git \
        libxslt-dev \
        libicu-dev \
        libmcrypt-dev \
        libxml2-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install -j$(nproc) iconv mcrypt mbstring mysqli pdo_mysql zip

RUN docker-php-ext-configure intl
RUN docker-php-ext-install -j$(nproc)  intl
RUN docker-php-ext-install -j$(nproc)  xsl
RUN docker-php-ext-install -j$(nproc)  soap

RUN apt-get install -y \
  libmagickwand-dev --no-install-recommends \
  && pecl install imagick \
  && docker-php-ext-enable imagick