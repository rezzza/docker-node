FROM rezzza/docker-node:6.2

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

ENV NPM_CONFIG_LOGLEVEL=warn \
    NPM_CONFIG_PROGRESS=false

RUN apk add --no-cache --virtual .build-app-deps \
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
    && npm config set spin=false \
    && npm config set loglevel=http \
    && npm install -g npm-shrinkwrap \
    && rm -rf \
        /usr/share/man \
        /tmp/* \
        /var/cache/apk/*

CMD [ "node" ]
