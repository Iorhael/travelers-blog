ARG ALPINE_VERSION=3.18

FROM alpine:$ALPINE_VERSION
ARG ALPINE_VERSION

ARG NGINX_PKEYHASH=ff7cf138acc09f2a5029300ab713fe6a1440605fca72e2bab76a4da9206fec87
ARG NGINX_VERSION=1.25.2
ARG NGINX_PKGREL=1

RUN set -eux \
\
&& addgroup -S -g 500 nginx && adduser -SDHG nginx -h /var/cache/nginx -s /sbin/nologin -u 500 nginx \
\
&& wget -qO /etc/apk/keys/nginx_signing.rsa.pub https://nginx.org/keys/nginx_signing.rsa.pub \
\
&& if [ "$(sha256sum /etc/apk/keys/nginx_signing.rsa.pub)" != "$NGINX_PKEYHASH  /etc/apk/keys/nginx_signing.rsa.pub" ]; then echo "key verification failed!"; exit 1; fi \
\
&& apk add --no-cache --repository "https://nginx.org/packages/mainline/alpine/v$ALPINE_VERSION/main" "nginx=$NGINX_VERSION-r$NGINX_PKGREL" \
\
&& rm -fv /etc/apk/keys/nginx_signing.rsa.pub \
\
&& ln -fs /dev/stderr /var/log/nginx/error.log \
&& ln -fs /dev/stdout /var/log/nginx/access.log \
\
&& mkdir /alwaysempty \
\
&& rm -r /etc/nginx \
&& mkdir /etc/nginx

ADD nginx /etc/nginx

EXPOSE 80

STOPSIGNAL SIGQUIT

CMD ["nginx", "-g", "daemon off;"]
