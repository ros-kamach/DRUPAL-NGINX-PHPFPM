FROM roskamach/centos_baseimage

MAINTAINER Rostylav Kamach <ros.kamach@gmail.com>

RUN yum update -y && \
    yum install -y \
    curl \
    git \
    unzip && \
    ### 
    yum clean all && \
    rm -rf /var/cache/yum

COPY ./drupal-8.7.4.zip /usr/share/nginx/

WORKDIR /usr/share/nginx/
RUN unzip drupal-8.7.4.zip && \
    rm -rf html drupal-8.7.4/.git && mv drupal-8.7.4/ html && rm drupal-8.7.4.zip && cd html/ && \
    ###
    curl -sS https://getcomposer.org/installer -o composer-setup.php && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    composer install --no-progress --profile --prefer-dist && \
    chown -R nginx:nginx /usr/share/nginx/html
COPY ./template/opcache /usr/share/nginx/opcache
RUN cat ./opcache >> /etc/php.ini && rm ./opcache
  

COPY ./template/default /etc/nginx/conf.d/default.conf

EXPOSE 80
ENTRYPOINT [ "script.sh" ]

