FROM php:7.4.33-fpm

WORKDIR /var/www/html

RUN apt-get update

# Libraries
RUN apt-get install -y --fix-missing \
    apt-utils \
    build-essential \
    git \
    curl \
    libcurl4 \
    libcurl4-openssl-dev \
    zlib1g-dev \
    libzip-dev \
    unzip zip \
    libbz2-dev \
    libmariadb-dev \
    locales \
    libmcrypt-dev \
    libicu-dev \
    libonig-dev \
    libxml2-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev

# PHP Extension
RUN docker-php-ext-install gettext intl pdo_mysql gd

RUN docker-php-ext-install \
    exif \
    pcntl \
    bcmath \
    ctype \
    curl \
    iconv \
    xml \
    soap \
    pcntl \
    mbstring \
    tokenizer \
    bz2 \
    zip

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg && docker-php-ext-install -j$(nproc) gd

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# NodeJS
RUN apt-get install -y nodejs npm

# Clear Cache
RUN apt-get clean && apt-get autoremove --purge && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*