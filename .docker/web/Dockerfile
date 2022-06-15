ARG PHP_VERSION

FROM php:${PHP_VERSION:+${PHP_VERSION}-}fpm
ARG COMPOSER_VERSION

LABEL maintainer="George Barbu"
LABEL version="1.x"
LABEL description="Development environment for the joy and pleasure of web developers"

RUN apt-get update && apt-get install -y \
    git \
    wget \
    zlib1g-dev \
    unixodbc \
    unixodbc-dev \
    freetds-dev \
    freetds-bin \
    tdsodbc \
    libicu-dev &&\
    rm -rf /var/lib/apt/lists/*;


# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo intl
RUN docker-php-ext-configure pdo_dblib --with-libdir=/lib/x86_64-linux-gnu

# install xdebug
RUN pecl install xdebug
RUN docker-php-ext-install pdo_dblib
RUN docker-php-ext-enable intl pdo_dblib

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer --version=${COMPOSER_VERSION}

COPY php.ini /usr/local/etc/php/php.ini

# Set working directory
WORKDIR /var/www
