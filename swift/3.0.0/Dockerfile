FROM ubuntu:15.10
MAINTAINER Adrian Brink <adrian@brink-holdings.com>

ENV USER root

ENV SWIFT_BRANCH swift-3.0-release
ENV SWIFT_VERSION swift-3.0-RELEASE
ENV SWIFT_PLATFORM ubuntu15.10

RUN apt-get update && \
    apt-get install -y build-essential wget clang-3.6 curl libedit-dev python2.7 python2.7-dev libicu-dev rsync libxml2 git libcurl4-openssl-dev && \
    update-alternatives --install /usr/bin/clang clang /usr/bin/clang-3.6 100 && \
    update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-3.6 100

RUN wget -q -O - https://swift.org/keys/all-keys.asc | gpg --import - && \
    gpg --keyserver hkp://pool.sks-keyservers.net --refresh-keys Swift

RUN SWIFT_ARCHIVE_NAME=$SWIFT_VERSION-$SWIFT_PLATFORM && \
    SWIFT_URL=https://swift.org/builds/$SWIFT_BRANCH/$(echo "$SWIFT_PLATFORM" | tr -d .)/$SWIFT_VERSION/$SWIFT_ARCHIVE_NAME.tar.gz && \
    wget $SWIFT_URL && \
    wget $SWIFT_URL.sig && \
    gpg --verify $SWIFT_ARCHIVE_NAME.tar.gz.sig && \
    tar -xvzf $SWIFT_ARCHIVE_NAME.tar.gz --directory / --strip-components=1 && \
    rm -rf $SWIFT_ARCHIVE_NAME*

RUN apt-get remove --purge -y wget && \
    apt-get autoclean && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV PATH /usr/bin:$PATH

VOLUME ["/source"]
WORKDIR /source
CMD ["/bin/bash"]