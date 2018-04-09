FROM php:5.6-apache
COPY php.ini /usr/local/etc/php/
RUN apt-get update \
  && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev libmcrypt-dev \
  && docker-php-ext-install pdo_mysql mysqli mbstring gd iconv mcrypt

#Resolve - debconf: delaying package configuration, since apt-utils is not installed
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

RUN apt-get update --fix-missing \
    && apt-get install -y curl wget zip unzip git \
    && rm -rf /var/lib/apt/lists/*

# DEPENDENCIES
RUN apt-get update --fix-missing \
    && apt-get install -y  python \
    && rm -rf /var/lib/apt/lists/*

# KAFKA
RUN git clone --depth 1 --branch v0.9.5 https://github.com/edenhill/librdkafka.git \
    && ( \
        cd librdkafka \
        && ./configure \
        && make \
        && make install \
    ) \
    && pecl install rdkafka \
    && echo "extension=rdkafka.so" > /usr/local/etc/php/conf.d/rdkafka.ini
