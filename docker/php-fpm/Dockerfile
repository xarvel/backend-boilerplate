FROM php:7-fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev

RUN docker-php-ext-install pdo

RUN apt-get update && apt-get install -y libpq-dev
RUN docker-php-ext-install pdo_pgsql

# Install Composer
RUN apt-get install -y git zip unzip
ENV COMPOSER_VERSION 1.2.0
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION}

# Install Xdebub
ENV XDEBUG_VERSION 2.4.1
ENV XDEBUG_SHA1 52b5cede5dcb815de469d671bfdc626aec8adee3

RUN set -x \
  	&& curl -SL "http://www.xdebug.org/files/xdebug-$XDEBUG_VERSION.tgz" -o xdebug.tgz \
  	&& echo $XDEBUG_SHA1 xdebug.tgz | sha1sum -c - \
  	&& mkdir -p /usr/src/xdebug \
  	&& tar -xf xdebug.tgz -C /usr/src/xdebug --strip-components=1 \
  	&& rm xdebug.* \
  	&& cd /usr/src/xdebug \
  	&& phpize \
  	&& ./configure \
  	&& make -j"$(nproc)" \
  	&& make install \
  	&& make clean

COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN mkdir -p /var/www

VOLUME /var/www

WORKDIR /var/www