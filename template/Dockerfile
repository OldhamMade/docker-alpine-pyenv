FROM oldhammade/alpine-pyenv:0.2

MAINTAINER Phillip B Oldham <info@oldhammade.net>

LABEL name="Alpine image containing pyenv" \
      description="Basic Alpine image plus pyenv." \
      distribution="alpine" \
      licence="MIT"

ARG PYTHON_INSTALL_VERSION
ENV VERSION_INSTALL_DIR="$PYENV_ROOT/versions/$PYTHON_INSTALL_VERSION"

RUN \
    pyenv install -v $PYTHON_INSTALL_VERSION && \
    pyenv global $PYTHON_INSTALL_VERSION && \
    echo "Reducing python install size" && \
    strip -s $VERSION_INSTALL_DIR/bin/python && \
    find $VERSION_INSTALL_DIR -type d -name "test*" -print0 | xargs -0 rm -rf && \
    rm -rf $VERSION_INSTALL_DIR/share/ && \
    echo "Precompiling stdlib .pyc files" && \
    $VERSION_INSTALL_DIR/bin/python -m compileall -f $VERSION_INSTALL_DIR && \
    pyenv rehash
