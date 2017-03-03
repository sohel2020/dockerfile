FROM ubuntu:14.04
MAINTAINER  Tarikur Rahaman <sohel2020@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get -y install \
    php5-curl \
    php5-mcrypt \
    php-apc \
    php-pear \
    php5-dev \
    php5-xdebug \
    php5-mysql \
    php5-pgsql \
    php5-cli \
    php5-mcrypt \
    php5-gd \
    php5-common \
    php5-fpm \
    php5-redis \
    supervisor \
    nginx 

RUN mkdir -p /var/www/html/public

COPY nginx-fpm.conf /etc/supervisor/conf.d/
COPY default /etc/nginx/sites-enabled/default 


# configure nginx and php-fpm as non-daemon
RUN echo "daemon off;" >> /etc/nginx/nginx.conf && \
    sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf
    
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod a+x /usr/local/bin/composer

# clear apt cache and remove unnecessary packages
RUN apt-get autoclean && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*


EXPOSE 80 443

CMD ["/usr/bin/supervisord"]

