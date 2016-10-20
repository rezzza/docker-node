FROM node:6.9.1

MAINTAINER Sébastien HOUZÉ <sebastien.houze@verylastroom.com>

ENV NPM_CONFIG_LOGLEVEL=warn \
    NPM_CONFIG_PROGRESS=false 

VOLUME /root/.yarn-cache

RUN curl -o- -L https://yarnpkg.com/install.sh | bash

CMD [ "node" ]
