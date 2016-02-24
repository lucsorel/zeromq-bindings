# Supported tags and `Dockerfile`s
* [alpinelinux3.3-zeromq4.3.x-pyzmq15.2.0](https://github.com/lucsorel/zeromq-bindings/tree/master/alpinelinux3.3-zeromq4.3.x-pyzmq15.2.0): (5 layers, [60 Mb](https://imagelayers.io/?images=lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-pyzmq15.2.0 'Alpine Linux-based Python image with ZeroMQ bindings'))
* [alpinelinux3.3-zeromq4.3.x-nodejs4.3.x](https://github.com/lucsorel/zeromq-bindings/tree/master/alpinelinux3.3-zeromq4.3.x-nodejs4.3.x): [![](https://badge.imagelayers.io/lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x.svg)](https://imagelayers.io/?images=lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x 'Alpine Linux-based NodeJS image with ZeroMQ bindings')
* [ubuntu15.10-zeromq4.1.x-nodejs4.3.x](https://github.com/lucsorel/zeromq-bindings/tree/master/ubuntu15.10-zeromq4.0-nodejs4.3.0): [![](https://badge.imagelayers.io/lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.0-nodejs4.3.0.svg)](https://imagelayers.io/?images=lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.0-nodejs4.3.0 'Ubuntu-based NodeJS image with ZeroMQ bindings')

# Images with ZeroMQ installation and bindings
## With bindings for Python applications
This image compiles the Python bindings from the official `py-zmq` projects and removes the packages involved in the compilation for image-size sake (5 layers, [60 Mb](https://imagelayers.io/?images=lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-pyzmq15.2.0 'Alpine Linux-based Python image with ZeroMQ bindings')).

A typical Dockerfile for a ZeroMQ-Python application would look like:

```
FROM lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-pyzmq15.2.0

# installs the Python application
RUN mkdir -p /usr/local/my-python-zeromq-app
WORKDIR /usr/local/my-python-zeromq-app
COPY preprocess.py /usr/local/my-python-zeromq-app/

# exposes tcp ports used by ZeroMQ sockets
EXPOSE 6969

# starts the application
CMD [ "python", "my-python-zeromq-app.py" ]
```

## With bindings for NodeJS applications
ZeroMQ bindings for NodeJS require `npm` and `Python 2.x` to be installed when your container runs the `npm i` command, which installs `zmq` via the `node-gyp` binding system. This is why these images are bigger than 'classic' NodeJS or ZeroMQ images.

* Ubuntu 15.10-based image with ZeroMQ 4.0.x and NodeJS 4.3.1 bindings (based on [ubuntu:15.10](https://hub.docker.com/_/ubuntu/) and [node:4.3.x](https://hub.docker.com/_/node/) images): [![](https://badge.imagelayers.io/lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.0-nodejs4.3.0.svg)](https://imagelayers.io/?images=lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.0-nodejs4.3.0 'Ubuntu-based NodeJS image with ZeroMQ bindings')

* Alpine Linux 3.3-based image with ZeroMQ 4.1.x and NodeJS 4.3.1 bindings (based on [Michael Hart's alpine-node image](https://hub.docker.com/r/mhart/alpine-node/)): [![](https://badge.imagelayers.io/lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x.svg)](https://imagelayers.io/?images=lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x 'Alpine Linux-based NodeJS image with ZeroMQ bindings')

A typical Dockerfile for a ZeroMQ-NodeJS application would look like:

```
# for an Alpine Linux-based image:
FROM lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-nodejs4.3.x
# or for an Ubuntu-based image:
# FROM lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.0-nodejs4.3.0

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
