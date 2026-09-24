FROM php:8.2-apache

# Библиотеки для расширений и русская локаль
RUN apt-get update && apt-get install -y --no-install-recommends \
        libicu-dev libonig-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
        locales \
    && sed -i 's/^# *\(ru_RU.UTF-8\)/\1/' /etc/locale.gen \
    && locale-gen \
    && rm -rf /var/lib/apt/lists/*

# intl нужен для вывода дат по-русски, gd — для генерации логотипа
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j"$(nproc)" intl mbstring gd opcache

RUN a2enmod rewrite \
    && sed -ri 's/AllowOverride None/AllowOverride All/g' /etc/apache2/apache2.conf

COPY php.ini /usr/local/etc/php/conf.d/zz-mysite.ini

WORKDIR /var/www/html
