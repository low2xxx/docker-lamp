FROM php:7.3-apache

RUN set -ex apk --no-cache add postgresql-dev libpq-dev

RUN apt-get update && apt-get install -y \
    vim curl less git unzip gcc make gnupg zlib1g-dev libpq-dev libzip-dev libmcrypt-dev libjpeg-dev libfreetype6-dev  \
    && docker-php-ext-install \
    zip mbstring pdo pdo_mysql pdo_pgsql mysqli -j$(nproc) gd\
    && docker-php-ext-enable mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && a2enmod rewrite

RUN curl -s http://getcomposer.org/installer | php && \
    echo "export PATH=${PATH}:/var/www/vendor/bin" >> ~/.bashrc && \
    mv composer.phar /usr/local/bin/composer

COPY ./php.ini /usr/local/etc/php/
