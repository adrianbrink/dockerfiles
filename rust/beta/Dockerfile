FROM debian:jessie
MAINTAINER Adrian Brink <adrian@brink-holdings.com>

ENV USER root

WORKDIR /root
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    build-essential ca-certificates curl

RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain beta -y

RUN apt-get remove --purge -y curl && \
    apt-get autoclean && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV PATH=/root/.cargo/bin:$PATH

VOLUME ["/source"]
WORKDIR /source
CMD ["/bin/bash"]