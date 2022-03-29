FROM php:5.6-apache
RUN apt-get update -y && apt-get install -y sendmail libpng-dev libzip-dev zip zlib1g-dev
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install zip
RUN docker-php-ext-install gd
RUN BEFORE_PWD=$(pwd) \
    && mkdir -p /opt/xdebug \
    && cd /opt/xdebug \
    && curl -k -L https://github.com/xdebug/xdebug/archive/XDEBUG_2_5_5.tar.gz | tar zx \
    && cd xdebug-XDEBUG_2_5_5 \
    && phpize \
    && ./configure --enable-xdebug \
    && make clean \
    && sed -i 's/-O2/-O0/g' Makefile \
    && make \
    && make install \
    && cd "${BEFORE_PWD}" \
    && rm -r /opt/xdebug
RUN docker-php-ext-enable xdebug
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini
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