FROM php:7.3-fpm
MAINTAINER SmartOps Academy <docker@smartops.academy>

RUN apt update \
 && apt -y full-upgrade \
 && apt install -y zip unzip htop \
 && apt install -y libjpeg62-turbo-dev libpng-dev libxml2-dev libzip-dev
RUN docker-php-source extract \
 && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
 && docker-php-ext-install mysqli opcache gd bcmath soap zip \
 && docker-php-ext-enable mysqli opcache gd bcmath soap zip
RUN pecl install redis \
 && docker-php-ext-enable redis
RUN cd /usr/src \
 && curl -o /usr/src/ioncube_loaders_lin_x86-64.tar.gz https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
 && tar xzf ioncube_loaders_lin_x86-64.tar.gz \
 && cp ioncube/ioncube_loader_lin_7.3.so /usr/local/lib/php/extensions/no-debug-non-zts-*/ \
 && rm -rf ioncube* \
 && docker-php-ext-enable ioncube_loader_lin_7.3
RUN apt purge -y libjpeg62-turbo-dev libpng-dev libxml2-dev libzip-dev \
 && apt install -y libcurl3-gnutls liberror-perl libexpat1 libjpeg62-turbo libpopt0 libx11-6 libx11-data libxau6 libxcb1 libxdmcp6 libxext6 libxmuu1 \
 && apt-get --purge -y autoremove \
 && apt-get clean \
 && docker-php-source delete

COPY ../etc/ /usr/local/etc/
COPY entrypoint.sh /

CMD ["/entrypoint.sh"]
