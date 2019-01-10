FROM oldhammade/alpine-glibc:3.7

MAINTAINER Phillip B Oldham <info@oldhammade.net>

LABEL name="Alpine image containing pyenv with glibc" \
      description="Basic Alpine image plus a blank pyenv, ready for you to install your own version of python. Based on frolvlad/alpine-glibc" \
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
libressl-dev \
patch \
readline-dev \
sqlite-dev \
tini \
zlib-dev \
"

RUN echo "ipv6" >> /etc/modules && \
    set -x && \
    apk update && \
    apk upgrade && \
    apk add --no-cache $PACKAGES || \
      (sed -i -e 's/dl-cdn/dl-4/g' /etc/apk/repositories && apk add --no-cache $PACKAGES) && \
    ln -s /usr/include/locale.h /usr/include/xlocale.h && \
    update-ca-certificates && \
    curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer \
      | sh && \
    apk del git && \
    rm -rf /var/cache/apk/* && \
    rm -rf /tmp/*

ENTRYPOINT ["/sbin/tini", "--"]
