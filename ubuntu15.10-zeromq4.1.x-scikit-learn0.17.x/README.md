# Image content
This Dockerfile produces an image:
* based on [Ubuntu](https://hub.docker.com/_/ubuntu/) [15.10](https://github.com/tianon/docker-brew-ubuntu-core/blob/e406914e5f648003dfe8329b512c30c9ad0d2f9c/wily/Dockerfile)
* with [ZeroMQ 4.3.x series from Chris Lea PPA](https://launchpad.net/~chris-lea/+archive/ubuntu/zeromq)
* with [scikit-learn stable](http://scikit-learn.org/stable/) (0.17.x) installed via `python pip`

# Image characteristics
* [![](https://badge.imagelayers.io/lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-scikit-learn0.17.x.svg)](https://imagelayers.io/?images=lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-scikit-learn0.17.x 'Ubuntu 15.10-based scikit-learn image with ZeroMQ bindings')
* [![](https://raw.githubusercontent.com/lucsorel/zeromq-bindings/master/docker-logo.png)](https://hub.docker.com/r/lucsorel/zeromq-bindings/ 'Hosted on Docker hub lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-scikit-learn0.17.x'): `FROM lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-scikit-learn0.17.x`

# Use it in your Dockerfile
A typical Dockerfile for a ZeroMQ/scikit-learn application would look like:

```dockerfile
FROM lucsorel/zeromq-bindings:ubuntu15.10-zeromq4.1.x-scikit-learn0.17.x

# installs the scikit-learn Python script
RUN mkdir -p /usr/local/data-mining
WORKDIR /usr/local/data-mining
COPY stream_analysis.py /usr/local/data-mining/

# exposes the tcp port used by the ZeroMQ socket
EXPOSE 6969

# starts the application
CMD [ "python", "stream_analysis.py" ]
```
