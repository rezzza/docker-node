FROM node:6.9.1-alpine

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

ENV NPM_CONFIG_LOGLEVEL=warn \
    NPM_CONFIG_PROGRESS=false \
    YARN_VERSION=0.18.0 \
    PATH=/home/node/.yarn/bin:$PATH

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
    && rm -rf \
        /usr/share/man \
        /tmp/* \
        /var/cache/apk/*

USER node

RUN mkdir -p ~/.yarn/bin \
    && curl --compressed -o ~/.yarn/bin/yarn -L https://github.com/yarnpkg/yarn/releases/download/v$YARN_VERSION/yarn-$YARN_VERSION.js \
    && chmod a+x ~/.yarn/bin/yarn \
    && npm config set spin=false \
    && npm config set loglevel=http \

CMD [ "node" ]
