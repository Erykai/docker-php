FROM php:7.2-apache
RUN docker-php-ext-install mysqli
RUN apt-get update -y && apt-get install -y sendmail libpng-dev
RUN apt-get update && \
    apt-get install -y \
        zlib1g-dev
RUN docker-php-ext-install zip
RUN docker-php-ext-install gd
RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
RUN chown -R root:www-data /var/www/html
RUN chmod u+rwx,g+rx,o+rx /var/www/html
RUN find /var/www/html -type d -exec chmod u+rwx,g+rx,o+rx {} +
RUN find /var/www/html -type f -exec chmod u+rw,g+rw,o+r {} +
WORKDIR /var/www/html
RUN a2enmod rewrite
RUN a2enmod ssl
EXPOSE 80
EXPOSE 443