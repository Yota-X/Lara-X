ARG  PHP_VERSION=${PHP_VERSION}

FROM php:${PHP_VERSION}-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libcurl4-openssl-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libmemcached-dev \
    libzip-dev \
    locales \
    libonig-dev \
    libwebp-dev \
    libsodium-dev \
    libpng-dev \
    libgmp-dev \
    zip \
    pkg-config \
    supervisor \
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
RUN docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype
RUN docker-php-ext-install -j$(nproc) gd pdo_mysql mysqli zip curl sodium gmp

# Create system user
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

CMD ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisor/supervisord.conf"]