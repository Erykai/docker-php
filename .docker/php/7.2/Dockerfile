FROM php:7.2-apache
RUN apt-get update -y && apt-get install -y sendmail libpng-dev libzip-dev zip zlib1g-dev ghostscript
#RUN mkdir -p /usr/src/php/ext/imagick; \
#    curl -fsSL https://github.com/Imagick/imagick/archive/06116aa24b76edaf6b1693198f79e6c295eda8a9.tar.gz | tar xvz -C "/usr/src/php/ext/imagick" --strip 1; \
#    docker-php-ext-install imagick;
RUN docker-php-ext-install mysqli pdo pdo_mysql zip gd opcache
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