FROM webdevops/apache:ubuntu-16.04

ARG PHP_SOCKET=php-fpm:9000

ENV WEB_PHP_SOCKET=$PHP_SOCKET

ENV WEB_DOCUMENT_ROOT=/var/www/upload

EXPOSE 80 443

WORKDIR /var/www/

ADD vhost.conf /etc/apache2/sites-enabled/vhost.conf

ENTRYPOINT ["/opt/docker/bin/entrypoint.sh"]

CMD ["supervisord"]
