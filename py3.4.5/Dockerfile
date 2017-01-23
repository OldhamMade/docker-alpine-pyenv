FROM oldhammade/alpine-pyenv:0.1

MAINTAINER Phillip B Oldham <info@oldhammade.net>

LABEL name="Alpine image containing pyenv" \
      description="Basic Alpine image plus pyenv with python versions: 3.4.5" \
      distribution="alpine" \
      licence="MIT"

ENV PYTHON_INSTALL_VERSION="3.4.5"
ENV VERSION_INSTALL_DIR="$PYENV_ROOT/versions/$PYTHON_INSTALL_VERSION"

RUN \
    pyenv install -v $PYTHON_INSTALL_VERSION && \
    pyenv global $PYTHON_INSTALL_VERSION && \
    echo "Reducing python install size" && \
    strip -s $VERSION_INSTALL_DIR/bin/python3 && \
    find $VERSION_INSTALL_DIR -type d -name "test*" -print0 | xargs -0 rm -rf && \
    rm -rf $VERSION_INSTALL_DIR/share/ && \
    echo "Precompiling stdlib .pyc files" && \
    $VERSION_INSTALL_DIR/bin/python3 -m compileall -f $VERSION_INSTALL_DIR && \
    pyenv rehash
