# docker build -t lucsorel/zeromq-bindings:alpinelinux3.3-zeromq4.3.x-pyzmq15.2.0 .
FROM alpine:3.3
MAINTAINER Luc Sorel

# comment to use the most recente version of py-zmq
ENV PYZMQ_VERSION="==15.2.0"

## installs
# - Python and Pip from Alpine 3.3 repositories
# - Python bindings for ZeroMQ with pip
RUN apk add --no-cache python && \
    apk add --no-cache --virtual=build-dependencies wget ca-certificates && \
    wget "https://bootstrap.pypa.io/get-pip.py" -O /dev/stdout | python && \
    apk add --no-cache python-dev gcc g++ zeromq && \
    pip install pyzmq${PYZMQ_VERSION} && \
    apk del build-dependencies python-dev gcc g++
