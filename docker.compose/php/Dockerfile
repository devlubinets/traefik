FROM php:7.4-fpm as php-xdebug-74

RUN pecl install xdebug-2.9.8 && docker-php-ext-enable xdebug

RUN apt-get -y update
RUN apt-get install -y libzip-dev && docker-php-ext-install zip
RUN apt-get install -y git libzip-dev libicu-dev && docker-php-ext-configure intl && docker-php-ext-install intl
RUN apt-get install -y libpng-dev zlib1g-dev && docker-php-ext-configure gd && docker-php-ext-install gd
RUN apt-get install -y curl && apt-get install -y libcurl4-gnutls-dev && docker-php-ext-install curl

RUN docker-php-ext-install json pdo pdo_mysql

RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

WORKDIR /usr/share/nginx/
CMD ["php-fpm"]