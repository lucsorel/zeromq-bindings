# Image content
This Dockerfile produces an image:
* based on [Alpine](https://hub.docker.com/_/alpine/) [3.3](https://github.com/tianon/docker-brew-ubuntu-core/blob/e406914e5f648003dfe8329b512c30c9ad0d2f9c/wily/Dockerfile)
* with `Nodejs 4.3.x` support based on [Mickael Hart's alpine-node image](https://github.com/mhart/alpine-node)
* with [ZeroMQ 4.1.x series](https://pkgs.alpinelinux.org/package/main/x86/zeromq)
* with `Python`, `make`, `gcc` and `g++` dependencies required by `node-gyp` when you `npm install` your NodeJS application with the `zmq` bindings package.

# Image characteristics
* [![](https://badge.imagelayers.io/lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x.svg)](https://imagelayers.io/?images=lucsorel/zeromq-containers:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x 'Alpine Linux-based NodeJS image with ZeroMQ bindings')
* [![](https://github.com/lucsorel/zeromq-bindings/blob/master/docker-logo.png)](https://hub.docker.com/r/lucsorel/zeromq-bindings/ 'Hosted on Docker hub lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x'): `FROM lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x`

# Use it in your Dockerfile
A typical Dockerfile for a ZeroMQ-NodeJS application would look like:

```dockerfile
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
