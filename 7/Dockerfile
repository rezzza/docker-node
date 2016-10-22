FROM alpine:edge

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

ENV NPM_CONFIG_LOGLEVEL=info \
        NODE_VERSION=7.0.0-pre \
        PATH=/root/.yarn/bin:$PATH

VOLUME /root/.yarn-cache

RUN apk upgrade --update-cache \
    && apk add --virtual .build-deps \
        gcc \
        g++ \
        libc-dev \
        make \
        python \
        linux-headers \
        zlib-dev \
        paxctl \
        binutils-gold \
        gnupg \
        curl \
        icu-dev \
        openssl-dev \
        pax-utils \
    && curl -SLO "https://nodejs.org/download/nightly/v7.0.0-nightly20161020d62e7bd1f9/node-v7.0.0-nightly20161020d62e7bd1f9.tar.xz" \
    && mkdir -p /usr/src \
    && tar -xJf "node-v7.0.0-nightly20161020d62e7bd1f9.tar.xz" -C /usr/src \
    && rm node-v7.0.0-nightly20161020d62e7bd1f9.tar.xz \
    && mv "/usr/src/node-v7.0.0-nightly20161020d62e7bd1f9" "/usr/src/node-v$NODE_VERSION" \
    && cd "/usr/src/node-v$NODE_VERSION" \
    && export GYP_DEFINES="linux_use_gold_flags=0" \
    && ./configure --prefix=/usr --with-intl=system-icu --shared-zlib --shared-openssl \
    && make -j$(getconf _NPROCESSORS_ONLN) -C out mksnapshot BUILDTYPE=Release \
    && paxctl -cm out/Release/mksnapshot \
    && make -j$(getconf _NPROCESSORS_ONLN) \
    && make install \
    && paxctl -cm /usr/bin/node \
    && cd / \
    && curl -o- -L https://yarnpkg.com/install.sh | ash \
    && runDeps="$( \
        scanelf --needed --nobanner --recursive /usr/bin/node /usr/lib/node* \
            | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
            | sort -u \
            | xargs -r apk info --installed \
            | sort -u )" \
    && apk add --virtual .node-rundeps $runDeps \
    && apk del --virtual .build-deps \
    && rm -rf \
        /usr/src/* \
        /usr/share/doc \
        /usr/share/man \
        /usr/share/doc \
        /tmp/* \
        /var/cache/apk/* \
        /root/.npm \
        /root/.node-gyp \
        /usr/lib/node_modules/npm/man \
        /usr/lib/node_modules/npm/doc \
        /usr/lib/node_modules/npm/html

CMD [ "node" ]
