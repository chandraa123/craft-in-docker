FROM php:8.1-fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev libjpeg62-turbo-dev \
        libpng-dev libbz2-dev \
        libssl-dev autoconf \
        ca-certificates curl g++ libicu-dev \
        libmagickwand-dev mariadb-client libzip-dev\
        && \
        pecl install imagick \
        && \
        docker-php-ext-install \
        bcmath bz2 exif \
        shmop sockets sysvmsg sysvsem sysvshm \
        zip iconv pdo_mysql intl \
        && \
        docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
        && \
        docker-php-ext-enable imagick

RUN apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer
RUN composer global config --no-plugins allow-plugins.hirak/prestissimo true

RUN echo "upload_max_filesize = 10M" > /usr/local/etc/php/php.ini && \
    echo "post_max_size = 10M" >> /usr/local/etc/php/php.ini && \
    echo "max_execution_time = 300" >> /usr/local/etc/php/php.ini && \
    echo "memory_limit = 256M" >> /usr/local/etc/php/php.ini

COPY --chown=www-data:www-data ./src /var/www/html

RUN composer update \
    composer install -d /var/www/html/ && \
    chown -R www-data:www-data /var/www/html/vendor && \
    chown -R www-data:www-data /var/www/html/composer.lock
