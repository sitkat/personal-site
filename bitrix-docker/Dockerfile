FROM php:8.2-apache

# Библиотеки, нужные расширениям PHP из требований 1С-Битрикс
RUN apt-get update && apt-get install -y --no-install-recommends \
        libfreetype6-dev libjpeg62-turbo-dev libpng-dev libwebp-dev \
        libzip-dev libxml2-dev libonig-dev libicu-dev libcurl4-openssl-dev \
        unzip msmtp \
    && rm -rf /var/lib/apt/lists/*

# Расширения PHP, которые проверяет мастер установки Битрикса
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install -j"$(nproc)" \
        mysqli pdo_mysql gd zip mbstring xml intl exif sockets bcmath opcache

# Битриксу нужен mod_rewrite и разрешённый .htaccess
RUN a2enmod rewrite headers expires \
    && sed -ri 's/AllowOverride None/AllowOverride All/g' /etc/apache2/apache2.conf

COPY php.ini /usr/local/etc/php/conf.d/zz-bitrix.ini

WORKDIR /var/www/html
