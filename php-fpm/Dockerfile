ARG  PHP_VERSION=${PHP_VERSION}

FROM php:${PHP_VERSION}-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libcurl4-openssl-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    freetds-bin \
    libpq-dev \
    freetds-dev \
    libtidy-dev \
    libxslt-dev \
    freetds-common \
    libsnmp-dev \
    libmemcached-dev \
    libzip-dev \
    locales \
    libc-client-dev \
    libkrb5-dev \
    libbz2-dev \
    libssl-dev \
    libonig-dev \
    libwebp-dev \
    libsodium-dev \
    libpng-dev \
    libgmp-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    pkg-config \
    jpegoptim \
    optipng \
    pngquant \
    gifsicle \
    vim \
    unzip \
    git \
    curl

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN ln -s /usr/lib/x86_64-linux-gnu/libsybdb.so /usr/lib/

RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype
RUN docker-php-ext-install -j$(nproc) \ 
    bcmath \
    bz2 \
    calendar \
    exif \
    gd \
    gettext \
    gmp \
    imap \
    intl \
    mysqli \
    pdo_dblib \
    pdo_mysql \
    pdo_pgsql \
    shmop \
    snmp \
    soap \
    sockets \
    sysvmsg \
    sysvsem \
    sysvshm \
    tidy \
    xsl 

# Install Redis plugin
RUN pecl install redis

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Create system user
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Set user for running
USER www

# Port exposing
EXPOSE 9000

CMD ["php-fpm"]