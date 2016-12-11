FROM debian:jessie
MAINTAINER Adrian Brink <adrian@brink-holdings.com>

ENV USER root

WORKDIR /root
RUN apt-get update && \
    apt-get install -y curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain stable -y

ENV PATH=/root/.cargo/bin:$PATH

RUN mkdir /source
COPY . /source
WORKDIR /source
CMD ["/bin/bash"]