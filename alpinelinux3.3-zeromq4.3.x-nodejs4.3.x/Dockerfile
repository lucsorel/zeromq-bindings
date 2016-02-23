# docker build -t lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x .
FROM mhart/alpine-node:4.3.1
MAINTAINER Luc Sorel

# installs ZeroMQ libraries and dependencies for the node-gyp binder, run while npm-installing your app
RUN apk add --no-cache make gcc g++ python zeromq zeromq-dev
