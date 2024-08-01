FROM php:8.1-fpm

WORKDIR /var/www

RUN rm -rf /var/www/html

RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libwebp-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libzip-dev \
    apt-utils \
    libonig-dev

RUN docker-php-ext-install zip pdo_mysql mbstring exif
RUN docker-php-ext-configure gd --with-webp --with-freetype=/usr/include/ --with-jpeg=/usr/include/
RUN docker-php-ext-install gd

# Install XDebug
RUN pecl install xdebug-3.3.2
RUN docker-php-ext-enable xdebug

# Install node 
RUN apt-get install -y nodejs && apt-get install -y npm

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN groupadd -g 1000 laravel
RUN useradd -u 1000 -ms /bin/bash -g laravel user

COPY --chown=user:laravel . /var/www

USER user

EXPOSE 9000

CMD ["php-fpm"]
