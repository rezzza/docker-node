FROM node:8.1.2-alpine

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

ENV FLOW_VERSION 0.49.1
ENV OCAML_VERSION 4.03.0
ENV PATH /home/node/.yarn/bin:$PATH

RUN apk add --no-cache --virtual .base-deps \
        libelf \
        tar \
    && apk add --no-cache --virtual .build-app-deps \
        bash \
        curl \
        git \
    && su node -lc "npm config set spin=false" \
    && apk add --no-cache --virtual .build-flow-deps \
        alpine-sdk \
        m4 \
        opam \
        lz4 \
        lz4-dev \
        libelf-dev \
        ncurses \
        inotify-tools \
        linux-headers \
        diffutils \
    && cd /tmp \
    && opam init --comp=$OCAML_VERSION \
    && eval `opam config env` \
    && opam install sedlex \
    && curl --compressed -SL https://github.com/facebook/flow/archive/v${FLOW_VERSION}.tar.gz -o /tmp/flow-${FLOW_VERSION}.tgz \
    && tar -C /tmp -xzpf /tmp/flow-${FLOW_VERSION}.tgz \
    && rm /tmp/flow-${FLOW_VERSION}.tgz \
    && cd /tmp/flow-${FLOW_VERSION} \
    && make -j"$(getconf _NPROCESSORS_ONLN)" \
    && cd / \
    && cp /tmp/flow-${FLOW_VERSION}/bin/flow /usr/local/bin \
    && rm -rf /tmp/* \
    && opam repository remove default \
    && rm -rf /root/.opam \
    && apk del .build-flow-deps

USER node

WORKDIR /home/node

CMD [ "node" ]
