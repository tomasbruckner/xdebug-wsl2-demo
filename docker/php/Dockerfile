FROM php:7.4-apache

RUN a2enmod rewrite

RUN apt-get update \
    && apt-get install -y git iproute2 libzip-dev zlib1g-dev \
    && apt-get clean

RUN docker-php-ext-install -j$(nproc) pdo_mysql zip

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && pecl clear-cache

COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY docker-php-entrypoint-modified /usr/local/bin/

RUN chmod +x /usr/local/bin/docker-php-entrypoint-modified

COPY 000-default.conf /etc/apache2/sites-available/

# xdebug
EXPOSE 9005

ENTRYPOINT ["docker-php-entrypoint-modified"]

CMD ["apache2-foreground"]
