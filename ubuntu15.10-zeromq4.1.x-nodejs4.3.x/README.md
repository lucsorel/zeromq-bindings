# Image content
This Dockerfile produces an image:
* based on [Ubuntu](https://hub.docker.com/_/ubuntu/) [15.10](https://github.com/tianon/docker-brew-ubuntu-core/blob/e406914e5f648003dfe8329b512c30c9ad0d2f9c/wily/Dockerfile)
* with [ZeroMQ 4.3.x series from Chris Lea PPA](https://launchpad.net/~chris-lea/+archive/ubuntu/zeromq)
* with [Nodejs](https://hub.docker.com/_/node/) [4.3.x](https://github.com/nodejs/docker-node/blob/0c722500f66fb5f606a57824babe9798ae98667b/4.3/Dockerfile)
* with `Python` (2.7), `make`, `gcc` and `g++` dependencies required by `node-gyp` when you `npm install` your NodeJS application with the `zmq` bindings package.

[![](https://badge.imagelayers.io/lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.0-nodejs4.3.0.svg)](https://imagelayers.io/?images=lucsorel/zeromq-containers:ubuntu15.10-zeromq4.0-nodejs4.3.0 'Ubuntu-based NodeJS container with ZeroMQ bindings')
