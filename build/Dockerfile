FROM php:7.4-fpm
# Install Composer
COPY --from=composer:1.10 /usr/bin/composer /usr/bin/composer

# Install PHP modules
RUN apt-get update && apt-get install -y git libpng-dev libjpeg-dev libwebp-dev zlib1g-dev libxml2-dev libzmq3-dev libzip-dev libbz2-dev zip unzip sudo \
    && docker-php-ext-install gd opcache mysqli pdo pdo_mysql bcmath sockets xmlrpc zip bz2 \
    && git clone https://github.com/mkoppanen/php-zmq.git \
    && cd php-zmq \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && docker-php-ext-enable zmq \
    && apt-get install -y libmagickwand-dev --no-install-recommends \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && rm -rf /var/lib/apt/lists/*