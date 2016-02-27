# Image content
This Dockerfile produces an image:
* based on [Ubuntu](https://hub.docker.com/_/ubuntu/) [15.10](https://github.com/tianon/docker-brew-ubuntu-core/blob/e406914e5f648003dfe8329b512c30c9ad0d2f9c/wily/Dockerfile)
* with [ZeroMQ 4.3.x series from Chris Lea PPA](https://launchpad.net/~chris-lea/+archive/ubuntu/zeromq)
* with [Nodejs](https://hub.docker.com/_/node/) [4.3.x](https://github.com/nodejs/docker-node/blob/0c722500f66fb5f606a57824babe9798ae98667b/4.3/Dockerfile)
* with `Python` (2.7), `make`, `gcc` and `g++` dependencies required by `node-gyp` when you `npm install` your NodeJS application with the `zmq` bindings package.

# Image characteristics
* [![](https://badge.imagelayers.io/lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-nodejs4.3.x.svg)](https://imagelayers.io/?images=lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-nodejs4.3.x 'Ubuntu-based NodeJS image with ZeroMQ bindings')
* [![](https://github.com/lucsorel/zeromq-bindings/blob/master/docker-logo.png)](https://hub.docker.com/r/lucsorel/zeromq-bindings/ 'Hosted on Docker hub lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-nodejs4.3.x'): `FROM lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-nodejs4.3.x`

# Use it in your Dockerfile
A typical Dockerfile for a ZeroMQ-NodeJS application would look like:

```dockerfile
# for an Alpine Linux-based image:
FROM lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x

# installs the NodeJS application and dependencies (including zmq - https://github.com/JustinTulloss/zeromq.node):
RUN mkdir -p /usr/local/my-nodejs-zeromq-app
WORKDIR /usr/local/my-nodejs-zeromq-app
COPY package.json server.js /usr/local/my-nodejs-zeromq-app/
RUN npm install
# copy static content folders
COPY www /usr/local/my-nodejs-zeromq-app/webapp/www

# exposes http and tcp ports used by ZeroMQ sockets
EXPOSE 3000
EXPOSE 6969

# starts the application
CMD [ "npm", "start" ]
```
