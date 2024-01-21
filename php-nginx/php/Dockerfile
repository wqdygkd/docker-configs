FROM php:7.4-fpm

ADD sources.list /etc/apt/

# php 源码扩展目录 /usr/src/php/ext/

# zip扩展所需的依赖扩展
RUN apt-get update && apt-get install -y zlib1g-dev && apt-get install -y libzip-dev
# gd扩展所需的依赖扩展
RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev

RUN docker-php-ext-install zip && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install pdo_mysql

# RUN docker-php-ext-enable zip
# RUN  docker-php-ext-install bcmath && docker-php-ext-enable bcmath && \
#         # docker-php-ext-install calendar && docker-php-ext-enable calendar && \
#         # docker-php-ext-install gd && docker-php-ext-enable gd && \
#         # docker-php-ext-install mcrypt && docker-php-ext-enable mcrypt && \
#         # docker-php-ext-install pdo_mysql && docker-php-ext-enable pdo_mysql && \
#         # docker-php-ext-install mysqli && docker-php-ext-enable mysqli && \
#         # docker-php-ext-install soap && docker-php-ext-enable soap && \
#         # docker-php-ext-install sockets && docker-php-ext-enable sockets && \
#         # docker-php-ext-install exif && docker-php-ext-enable exif && \
#         # docker-php-ext-install wddx && docker-php-ext-enable wddx && \
#         # docker-php-ext-install wmlrpc && docker-php-ext-enable wmlrpc && \
#         docker-php-ext-install zip && docker-php-ext-enable zip
