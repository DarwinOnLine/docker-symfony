FROM debian:jessie
ARG SITE_URL

MAINTAINER Matthieu POIGNANT <matthieu.poignant@gmail.com>

RUN apt-get update && apt-get install -y \
    nginx

ADD nginx.conf /etc/nginx/
ADD symfony.conf /etc/nginx/sites-available/
RUN sed -i "s|\$SITE_URL|${SITE_URL}|g" /etc/nginx/sites-available/symfony.conf

RUN ln -s /etc/nginx/sites-available/symfony.conf /etc/nginx/sites-enabled/symfony
RUN rm /etc/nginx/sites-enabled/default

RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
