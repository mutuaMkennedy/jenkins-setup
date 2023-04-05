FROM nginxinc/nginx-unprivileged:1-alpine
LABEL maintainer="www.kennedymutua.crunchgarage.com"

COPY ./run.sh /run.sh

USER root

RUN apk add --no-cache certbot && apk add certbot-nginx

RUN chown nginx:nginx /etc/nginx/conf.d/default.conf && \
    chmod +x /run.sh

USER nginx

CMD ["/run.sh"]