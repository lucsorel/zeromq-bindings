# Image content
This Dockerfile produces an image:
* based on [Alpine](https://hub.docker.com/_/alpine/) [3.3](https://github.com/tianon/docker-brew-ubuntu-core/blob/e406914e5f648003dfe8329b512c30c9ad0d2f9c/wily/Dockerfile)
* with `Python 2.x`
* with [ZeroMQ 4.1.x series](https://pkgs.alpinelinux.org/package/main/x86/zeromq) bindings based on the official [py-zmq bindings](https://pyzmq.readthedocs.org/) installed with `pip`.

[![](https://badge.imagelayers.io/lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-pyzmq15.2.0.svg)](https://imagelayers.io/?images=lucsorel/zeromq-containers:alpinelinux3.3-zeromq4.3.x-pyzmq15.2.0 'Alpine Linux-based Python image with ZeroMQ bindings')

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