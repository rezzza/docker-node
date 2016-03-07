FROM rezzza/docker-node:5.7.1

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

EXPOSE 3000

RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && apk upgrade --update-cache \
    && apk add --virtual .run-deps \
        libmcrypt \
    && apk add --virtual .build-app-deps \
        curl \
        bash \
        git \
        make \
        automake \
        autoconf \
        nasm \
        gcc \
        g++ \
        openjdk8-jre \
        libelf-dev \
        binutils-gold \
        libgcc \
        libstdc++ \
        python \
        libmcrypt-dev \
        libpng-dev \
        libpng \
        libjpeg-turbo-dev \
        jpeg-dev \
    && apk add \
        ocaml@testing \
    && npm config set spin=false \
    && npm config set loglevel=http \
    && rm -rf \
        /usr/share/man \
        /tmp/* \
        /var/cache/apk/*

CMD [ "node" ]
