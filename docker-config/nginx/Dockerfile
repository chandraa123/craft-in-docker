FROM ubuntu/nginx

WORKDIR /home/ubuntu/craft-in-docker/docker-config/nginx/
COPY default.conf /etc/nginx/conf.d/default.conf

WORKDIR /home/ubuntu/craft-in-docker/src/
COPY --chown=www-data:www-data web/* /var/www/html/web/
