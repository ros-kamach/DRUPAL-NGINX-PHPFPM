FROM roskamach/centos_baseimage

MAINTAINER Rostylav Kamach <ros.kamach@gmail.com>

COPY ./drupal-8.7.5.zip /usr/share/nginx/
COPY ./template/opcache /usr/share/nginx/opcache
COPY ./template/default /etc/nginx/conf.d/default.conf
COPY ./template/10-opcache.ini /etc/php.d/10-opcache.in

WORKDIR /usr/share/nginx/

RUN yum update -y && \
    yum install -y \
    curl \
    git \
    unzip \
    php-dom \
    php-gd \
    php-pdo \
    php-xml \
    php-mysql \
    php-simplexml \
    php-mbstring \
    php-curl \
    php-opcache \
    ###
    php-cli && \
    #1php-common && \
    #php-cgi \
    #1php-json && \
    #php-intl && \
    ###
    unzip drupal-8.7.5.zip && \
    rm -rf html drupal-8.7.5/.git && mv drupal-8.7.5/ html && rm drupal-8.7.5.zip && cd html/ && \
    ###
    curl -sS https://getcomposer.org/installer -o composer-setup.php && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    ###
    composer install --no-progress --profile --prefer-dist && \
    ### 
    yum clean all && \
    rm -rf /var/cache/yum /var/tmp/yum-* /home/*/.composer/cache /root/.composer/cache && \
    chown -R nginx:nginx /usr/share/nginx/html && \
    cat ../opcache >> /etc/php.ini && rm ../opcache
  

EXPOSE 80
ENTRYPOINT [ "script.sh" ]

