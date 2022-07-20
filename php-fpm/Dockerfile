FROM php:8.1-fpm-alpine

RUN apk add --no-cache libzip-dev zlib-dev libpng-dev libjpeg-turbo-dev freetype-dev \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) zip gd mysqli

CMD ["php-fpm"]

EXPOSE 9000
