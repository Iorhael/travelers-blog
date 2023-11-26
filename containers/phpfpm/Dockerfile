ARG ALPINE_VERSION=3.18

FROM alpine:$ALPINE_VERSION
ARG ALPINE_VERSION

RUN set -eux \
\
&& addgroup -S -g 600 phpfpm && adduser -SDHG phpfpm -h /var/cache/phpfpm -s /sbin/nologin -u 600 phpfpm \
\
&& apk add --no-cache php82-fpm \
\
&& rm -r /etc/php82/php-fpm.d \
&& mkdir /etc/php82/php-fpm.d \
\
&& rm /etc/php82/php-fpm.conf

ADD php /etc/php82

CMD ["php-fpm82", "--nodaemonize"]
