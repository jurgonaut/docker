FROM alpine:latest

# Install dependencies
RUN apk add --no-cache \
    apache2 \
    php7 \
    php7-apache2 \
    php7-mysqli \
    php7-ctype \
    php7-curl \
    php7-dom \
    php7-fileinfo \
    php7-ftp \
    php7-iconv \
    php7-json \
    php7-mbstring \
    php7-mysqlnd \
    php7-openssl \
    php7-pdo \
    php7-pdo_sqlite \
    php7-pear \
    php7-phar \
    php7-posix \
    php7-session \
    php7-simplexml \
    php7-sqlite3 \
    php7-tokenizer \
    php7-xml \
    php7-xmlreader \
    php7-xmlwriter \
    php7-zlib

# Debuging dependencies
#RUN apk add --no-cache \
#    bash \
#    nano

# Set some envoirnment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

# Make a folder for apache2 process pid
RUN mkdir -p /run/apache2

# Copy example index.php
RUN rm /var/www/localhost/htdocs/index.html
COPY index.php /var/www/localhost/htdocs

# TODO: add apache conf
# TODO: add php conf
# TOTD: add php-fpm

# Expose port and run web server in foreground to prevend exiting
EXPOSE 80
CMD ["httpd", "-D", "FOREGROUND"]