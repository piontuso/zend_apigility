FROM php:7.1-apache

RUN apt-get update && apt-get install --no-install-recommends  -y \
    pkg-config \
    mcrypt \
    unzip \
    wget

#PHP Extensions
RUN pecl install xdebug && docker-php-ext-enable xdebug \
  && docker-php-ext-enable opcache

#Set the timezone.
RUN echo "Europe/Warsaw" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata
#XDEBUG
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini
RUN a2enmod rewrite
#COMPOSER
RUN wget https://getcomposer.org/download/1.4.1/composer.phar -O /usr/bin/composer && chmod +x /usr/bin/composer
RUN mkdir /composer
#VIM
RUN apt-get install -y vim
#NET-TOOLS
RUN apt-get install -y net-tools
# SET APACHE DOCUMENT ROOT
ENV DOCUMENT_ROOT /var/www/html
RUN sed -ri -e 's!/var/www/html!${DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
RUN apt-get clean && rm -rf /vsar/lib/apt/lists/* /tmp/* /var/tmp/*