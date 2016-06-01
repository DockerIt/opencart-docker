FROM nginx:latest

MAINTAINER Matthew Tonkin-Dunn <mattythebatty@gmail.com>

ADD nginx.conf /etc/nginx/
ADD opencart.conf /etc/nginx/sites-available/

RUN echo "upstream php-upstream { server php-fpm:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80 443
