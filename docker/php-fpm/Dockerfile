FROM php:7.3-fpm-alpine

RUN echo "Asia/Jakarta" > /etc/timezone

## gettext
RUN apk add --update --no-cache pcre-dev ${PHPIZE_DEPS} \
    gettext-dev \
    libintl icu icu-dev \
    zlib-dev libzip-dev \
    postgresql-dev \
    libmcrypt-dev libmcrypt \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    gmp gmp-dev \
    autoconf g++ imagemagick-dev libtool make pcre-dev \
    && pecl install mcrypt-1.0.2 imagick \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gettext intl zip mysqli pdo_mysql pdo_pgsql gmp bcmath gd \
    && docker-php-ext-enable mcrypt imagick

RUN apk add --update --no-cache curl \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
    && composer config -g repos.packagist composer https://packagist.phpindonesia.id \
    && composer global require hirak/prestissimo

RUN apk del postgresql-dev autoconf g++ libtool make pcre-dev \
    && apk add --upgrade postgresql --update-cache \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR "/application"
