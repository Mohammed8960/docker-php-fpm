FROM php:7-fpm
RUN apt-get update \
  && apt-get install -y \
    cron \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libxslt1-dev

RUN apt-get install -y libmcrypt-dev \
	&& rm -rf /var/lib/apt/lists/* \
	&& pecl install mcrypt-1.0.1 \
	&& docker-php-ext-enable mcrypt


RUN docker-php-ext-configure \
  gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install \
  bcmath \
  gd \
  intl \
  mbstring \
  pdo_mysql \
  soap \
  xsl \
  zip

RUN curl -sS https://getcomposer.org/installer | \
  php -- --install-dir=/usr/local/bin --filename=composer

ENV PHP_MEMORY_LIMIT 2G
ENV PHP_PORT 9000
ENV PHP_PM dynamic
ENV PHP_PM_MAX_CHILDREN 10
ENV PHP_PM_START_SERVERS 4
ENV PHP_PM_MIN_SPARE_SERVERS 2
ENV PHP_PM_MAX_SPARE_SERVERS 6
ENV APP_MAGE_MODE default

# COPY conf/www.conf /usr/local/etc/php-fpm.d/
# COPY conf/php.ini /usr/local/etc/php/
# COPY conf/php-fpm.conf /usr/local/etc/
# COPY bin/* /usr/local/bin/

# CMD ["/usr/local/bin/start"]


RUN echo "memory_limit=2048M" > /usr/local/etc/php/conf.d/magento.ini \
    && echo "realpath_cache_size=2M" >> /usr/local/etc/php/conf.d/magento.ini \
    && echo "opcache.max_accelerated_files=200000" >> /usr/local/etc/php/conf.d/magento.ini \
    && echo "opcache.memory_consumption=256M" >> /usr/local/etc/php/conf.d/magento.ini \
    && echo "zlib.output_compression=1" >> /usr/local/etc/php/conf.d/magento.ini