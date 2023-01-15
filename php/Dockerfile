FROM php:8.1-fpm

ENV TOKEN_ACCESS ""

RUN apt update \
    && apt install -y zlib1g-dev g++ git libicu-dev zip libzip-dev zip \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

WORKDIR /var/www/symfony_docker

# Packages
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        git \
        zlib1g-dev \
        unzip \
        python \
        && ( \
            cd /tmp \
            && mkdir librdkafka \
            && cd librdkafka \
            && git clone https://github.com/edenhill/librdkafka.git . \
            && ./configure \
            && make \
            && make install \
        ) \
    && rm -r /var/lib/apt/lists/*

# PHP Extensions
RUN docker-php-ext-install -j$(nproc) zip \
    && ( \
            cd /tmp \
            && mkdir php-rdkafka \
            && cd php-rdkafka \
            && git clone --depth 1 --branch 5.0.2 https://github.com/arnaud-lb/php-rdkafka.git . \
            && phpize \
            && ./configure \
            && make all -j 5 \
            && make install \
        ) \
    && docker-php-ext-enable rdkafka

RUN apt-get update -y && apt-get install -y libpng-dev  libjpeg-dev libfreetype6-dev

#RUN docker-php-ext-install gd
#RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr --with-png-dir=/usr \
 # && docker-php-ext-install -j "$(nproc)" gd

RUN docker-php-ext-configure gd --with-jpeg=/usr/include/ --with-freetype=/usr/include/ && docker-php-ext-install gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony
RUN git config --global user.email "micheenkusu1367@gmail.com" \ 
    && git config --global user.name "Michee NKUSU"
