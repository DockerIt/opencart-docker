FROM php:7.0-apache

MAINTAINER Matthew Tonkin-Dunn <mattythebatty@gmail.com>

RUN apt-get update && apt-get install -y \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libmcrypt-dev \
	libpng12-dev \
    curl

# Install extensions using the helper script provided by the base image
RUN docker-php-ext-install \
	zip \
	mcrypt \
	pdo_mysql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd

RUN usermod -u 1000 www-data
RUN a2enmod rewrite

ADD apache2.conf /etc/apache2/apache2.conf

WORKDIR /var/www/opencart

EXPOSE 80
CMD ["apache2-foreground"]
