FROM rezzza/docker-node:6.0.0

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

EXPOSE 3000

RUN apk upgrade --update-cache \
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
        binutils-gold \
        libgcc \
        libstdc++ \
        python \
        libpng-dev \
        libpng \
        jpeg-dev \
    && npm config set spin=false \
    && npm config set loglevel=http \
    && rm -rf \
        /usr/share/man \
        /tmp/* \
        /var/cache/apk/*

CMD [ "node" ]
