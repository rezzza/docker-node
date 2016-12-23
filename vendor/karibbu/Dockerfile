FROM rezzza/docker-node:6.9.2

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

ENV YARN_VERSION 0.18.1
ENV FLOW_VERSION=0.37.4
ENV PATH /home/node/.yarn/bin:$PATH

COPY flow.patch /tmp/

RUN apk add --no-cache --virtual .base-deps \
        libelf \
        tar \
    && apk add --no-cache --virtual .build-app-deps \
        bash \
        curl \
    && sed -i -e 's/v3\.4/edge/g' /etc/apk/repositories \
    && apk add --no-cache --virtual .build-flow-deps \
        alpine-sdk \
        ocaml \
        lz4 \
        lz4-dev \
        ocamlbuild \
        libelf-dev \
        ncurses \
        inotify-tools \
        linux-headers \
        diffutils \
    && cd /tmp \
    && curl -SL https://github.com/facebook/flow/archive/v${FLOW_VERSION}.tar.gz -o /tmp/flow-${FLOW_VERSION}.tgz \
    && tar -C /tmp -xzpf /tmp/flow-${FLOW_VERSION}.tgz \
    && rm /tmp/flow-${FLOW_VERSION}.tgz \
    && cd /tmp/flow-${FLOW_VERSION} \
    && cp /tmp/flow.patch . \
    && git apply flow.patch \
    && make -j"$(getconf _NPROCESSORS_ONLN)" \
    && cd / \
    && cp /tmp/flow-${FLOW_VERSION}/bin/flow /usr/local/bin \
    && rm -rf /tmp/* \
    && apk del .build-flow-deps \
    && sed -i -e 's/edge/v3\.4/g' /etc/apk/repositories

USER node

WORKDIR /home/node

RUN mkdir -p ~/.yarn/bin \
    && curl --compressed -o ~/.yarn/bin/yarn -L https://github.com/yarnpkg/yarn/releases/download/v$YARN_VERSION/yarn-$YARN_VERSION.js \
    && chmod a+x ~/.yarn/bin/yarn \
    && npm config set spin=false

CMD [ "node" ]
