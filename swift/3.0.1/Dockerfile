FROM ubuntu:16.04
MAINTAINER Adrian Brink <adrian@brink-holdings.com>

ENV USER root

ENV SWIFT_BRANCH swift-3.0.1-release
ENV SWIFT_VERSION swift-3.0.1-RELEASE
ENV SWIFT_PLATFORM ubuntu16.04

RUN apt-get update && \
    apt-get install -y clang libicu-dev wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q -O - https://swift.org/keys/all-keys.asc | gpg --import - && \
    gpg --keyserver hkp://pool.sks-keyservers.net --refresh-keys Swift

RUN SWIFT_ARCHIVE_NAME=$SWIFT_VERSION-$SWIFT_PLATFORM && \
    SWIFT_URL=https://swift.org/builds/$SWIFT_BRANCH/$(echo "$SWIFT_PLATFORM" | tr -d .)/$SWIFT_VERSION/$SWIFT_ARCHIVE_NAME.tar.gz && \
    wget $SWIFT_URL && \
    wget $SWIFT_URL.sig && \
    gpg --verify $SWIFT_ARCHIVE_NAME.tar.gz.sig && \
    tar -xvzf $SWIFT_ARCHIVE_NAME.tar.gz --directory / --strip-components=1 && \
    rm -rf $SWIFT_ARCHIVE_NAME* /tmp/* /var/tmp/*

ENV PATH /usr/bin:$PATH

RUN mkdir /source
COPY . /source
WORKDIR /source
CMD ["/bin/bash"]