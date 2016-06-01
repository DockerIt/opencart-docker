FROM php:7.0-fpm

MAINTAINER Matthew Tonkin-Dunn <mattythebatty@gmail.com>

ADD ./opencart.ini /usr/local/etc/php/conf.d
ADD ./opencart.pool.conf /usr/local/etc/php-fpm.d/

RUN apt-get update && apt-get install -y \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libmcrypt-dev \
	libpng12-dev \
    curl

# Install extensions using the helper script provided by the base image
RUN docker-php-ext-install \
	gd \
	zip \
	mcrypt \
	pdo_mysql

RUN usermod -u 1000 www-data

WORKDIR /var/www/opencart

CMD ["php-fpm"]

EXPOSE 9000
