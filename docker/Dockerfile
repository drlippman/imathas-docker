FROM php:8.1-apache
	
	RUN pecl install xdebug-3.3.1 \
		&& docker-php-ext-enable xdebug \
        && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
        && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
        && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini \
        && echo "xdebug.remote_host=docker.for.mac.localhost" >> /usr/local/etc/php/conf.d/xdebug.ini
	RUN a2enmod rewrite
	RUN docker-php-ext-install pdo pdo_mysql gettext
	RUN apt-get update && \
        apt-get install -y libfreetype-dev libjpeg62-turbo-dev libpng-dev && \
        docker-php-ext-configure gd --with-freetype --with-jpeg && \
        docker-php-ext-install gd
    RUN apt-get install -y \
            libzip-dev \
            zip \
      && docker-php-ext-install zip
    RUN cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-enabled/
	RUN a2enmod ssl
	RUN apt-get purge -y javascript-common

