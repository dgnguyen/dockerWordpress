FROM php:5.6-fpm

# install the PHP extensions we need
RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y \
		libjpeg-dev \
		libpng12-dev \
                libmcrypt-dev \
                ssmtp \
	; \
	rm -rf /var/lib/apt/lists/*; \
	\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	docker-php-ext-install gd mysqli opcache pdo_mysql json mcrypt; \
        pecl install -o -f redis \
        && rm -rf /tmp/pear \
        && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini;
# TODO consider removing the *-dev deps and only keeping the necessary lib* packages

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini



RUN { \
        echo 'error_reporting  =  E_ALL'; \
        echo 'log_errors = On'; \
        echo 'display_errors = Off'; \
    } > /usr/local/etc/php/php.ini

CMD ["php-fpm"]
EXPOSE 9000
