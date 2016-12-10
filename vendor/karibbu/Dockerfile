FROM rezzza/docker-node:6.9.2

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

ENV YARN_VERSION 0.18.0
ENV PATH /home/node/.yarn/bin:$PATH
ENV SASS_BINARY_PATH=/home/node/node-sass-binding.node
ENV SKIP_SASS_BINARY_DOWNLOAD_FOR_CI=true

RUN apk add --no-cache --virtual .build-app-deps \
        bash \
        curl \
        tar

USER node

WORKDIR /home/node

ADD node-sass-binding.node /home/node

RUN mkdir -p ~/.yarn/bin \
    && curl --compressed -o ~/.yarn/bin/yarn -L https://github.com/yarnpkg/yarn/releases/download/v$YARN_VERSION/yarn-$YARN_VERSION.js \
    && chmod a+x ~/.yarn/bin/yarn \
    && npm config set spin=false

CMD [ "node" ]
