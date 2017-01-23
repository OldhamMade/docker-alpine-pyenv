FROM alpine:3.4

MAINTAINER Phillip B Oldham <info@oldhammade.net>

LABEL name="Alpine image containing pyenv" \
      description="Basic Alpine image plus a blank pyenv, ready for you to install your own version of python" \
      distribution="alpine" \
      licence="MIT"

# ENV SHELL=/bin/bash

# distutils builds C++ extensions with g++, so provid the full path
ENV CXX="/usr/bin/g++"

# pyenv
ENV PYENV_ROOT="/usr/local/pyenv"
ENV PYENV_VIRTUALENV_ROOT="$PYENV_ROOT/plugins/pyenv-virtualenv"
ENV PATH="$PYENV_VIRTUALENV_ROOT/shims:$PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH"

ENV PACKAGES="\
bash \
bash-completion \
build-base \
bzip2-dev \
ca-certificates \
curl \
tini \
gcc \
g++ \
git \
linux-headers \
ncurses-dev \
openssl-dev \
patch \
readline-dev \
sqlite-dev \
zlib-dev \
"

RUN echo "ipv6" >> /etc/modules && \
    set -x && \
    sed -i -e 's/v3\.4/edge/g' /etc/apk/repositories && \
    apk update && \
    apk upgrade && \
    apk add --no-cache $PACKAGES || \
      (sed -i -e 's/dl-cdn/dl-4/g' /etc/apk/repositories && apk add --no-cache $PACKAGES) && \
    mv /usr/bin/tini /sbin/init && \
    ln -s /usr/include/locale.h /usr/include/xlocale.h && \
    update-ca-certificates && \
    curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer \
      | sh && \
    apk del curl git && \
    rm -rf /var/cache/apk/* && \
    rm -rf /tmp/*

ENTRYPOINT ["/sbin/tini", "--"]
