FROM node:6.9.1-alpine

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

ENV NPM_CONFIG_LOGLEVEL=warn \
    NPM_CONFIG_PROGRESS=false \
    PATH=/var/cache/node/.yarn/bin:$PATH

RUN apk add --no-cache --virtual .build-app-deps \
        autoconf \
        automake \
        bash \
        binutils-gold \
        curl \
        g++ \
        gcc \
        git \
        libgcc \
        libstdc++ \
        make \
        nasm \
        python \
        tar \
    && cd / \
    && rm -rf \
        /usr/share/man \
        /tmp/* \
        /var/cache/apk/*

USER node

RUN curl -o- -L https://yarnpkg.com/install.sh | ash \
    && npm config set spin=false \
    && npm config set loglevel=http \

CMD [ "node" ]
