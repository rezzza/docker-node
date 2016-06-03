FROM rezzza/docker-node:6.2

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

EXPOSE 3000

ENV NPM_CONFIG_LOGLEVEL=warn \
    NPM_CONFIG_PROGRESS=false

RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && cat /etc/apk/repositories \
    && apk add --no-cache --virtual .build-app-deps \
        curl \
        bash \
        git \
        make \
        automake \
        autoconf \
        nasm \
        gcc \
        g++ \
        binutils-gold \
        libgcc \
        libstdc++ \
    && apk add --no-cache \
        libsass@testing \
    && npm config set spin=false \
    && npm config set loglevel=http \
    && rm -rf \
        /usr/share/man \
        /tmp/* \
        /var/cache/apk/*

CMD [ "node" ]
