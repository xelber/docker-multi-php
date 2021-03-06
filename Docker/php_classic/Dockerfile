ARG CLASSIC_PHP_VERSION=7.1
FROM php:$CLASSIC_PHP_VERSION-fpm

ARG WITH_XDEBUG=0
ENV WITH_XDEBUG $WITH_XDEBUG
ARG GIT_USER
ENV GIT_USER $GIT_USER
ARG GIT_EMAIL
ENV GIT_EMAIL $GIT_EMAIL

RUN apt-get update && apt-get install -y \
        vim \
        wget \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libmcrypt-dev \
        libzip-dev \
        zlib1g-dev libicu-dev g++ \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install calendar \
    && docker-php-ext-install zip


COPY php.ini /usr/local/etc/php/conf.d/php.ini

RUN curl https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN if [ "$WITH_XDEBUG" = "1" ] ; then pecl install xdebug; docker-php-ext-enable xdebug; fi
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN git config --global user.email "$GIT_EMAIL"
RUN git config --global user.name "$GIT_USER"

RUN apt-get install -y npm
RUN docker-php-ext-install intl

RUN pecl channel-update pecl.php.net
RUN pecl install -f mcrypt-1.0.1
COPY mcrypt.ini /usr/local/etc/php/conf.d/mcrypt.ini
