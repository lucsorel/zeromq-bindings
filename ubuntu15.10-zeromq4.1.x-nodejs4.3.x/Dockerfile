## Image built with:
# docker build -t lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-nodejs4.3.x .
FROM ubuntu:15.10
MAINTAINER Luc Sorel

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 4.3.1

# install:
# - setup dependencies (cleaned up at the end)
# - ZeroMQ
# - NodeJS 4.3.1 (gpg keys listed at https://github.com/nodejs/node)
# - Python, make, gcc and g++ dependencies required for NodeJS apps requiring node-gyp bindings
RUN apt-get update && apt-get install -y --no-install-recommends software-properties-common curl && \
    add-apt-repository -y ppa:chris-lea/zeromq && \
    add-apt-repository -y ppa:chris-lea/libpgm && \
    apt-get update && \
    apt-get install -y libzmq3 libzmq3-dev python make gcc g++ && \
    set -ex && for key in \
        9554F04D7259F04124DE6B476D5A82AC7E37093B \
        94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
        0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
        FD3A5288F042B6850C66B31F09FE44734EB7990E \
        71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
        DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
        B9AE9905FFD7803F25714661B63B535A4C206CA9 \
        C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
      ; do \
        gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
    done && \
    curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" && \
    curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" && \
    gpg --verify SHASUMS256.txt.asc && \
    grep " node-v$NODE_VERSION-linux-x64.tar.gz\$" SHASUMS256.txt.asc | sha256sum -c - && \
    tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 && \
    rm "node-v$NODE_VERSION-linux-x64.tar.gz" SHASUMS256.txt.asc && \
    apt-get remove -y software-properties-common curl && \
    apt-get autoremove -y
