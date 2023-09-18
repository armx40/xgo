# Go cross compiler (xgo): Base cross-compilation layer
# Copyright (c) 2014 Péter Szilágyi. All rights reserved.
#
# Released under the MIT license.
ARG VERSION=latest
FROM xgo-${VERSION}-base

LABEL maintainer="techknowlogick <techknowlogick@gitea.io>"

COPY go.mod /xgo-src/
COPY xgo.go /xgo-src/

# Mark the image as xgo enabled to support xgo-in-xgo
ENV XGO_IN_XGO 1

# Install xgo within the container to enable internal cross compilation
WORKDIR /xgo-src
RUN \
  echo "Installing xgo-in-xgo..." && \
  go install xgo.go && \
  ln -s /go/bin/xgo /usr/bin/xgo && \
  rm -r /xgo-src

WORKDIR /

# Inject the container entry point, the build script
COPY build.sh /build.sh
ENV BUILD /build.sh
RUN chmod +x "$BUILD"


# install project specifics

RUN apt update
RUN apt install -y libczmq4
RUN apt install -y libczmq-dev
RUN apt install -y libzmq3-dev
RUN apt install -y libsodium-dev
RUN apt install -y libvips-dev
RUN apt install -y libusb-dev
RUN apt install -y libusb-1.0-0
RUN apt install -y libusb-1.0-0-dev
RUN dpkg --add-architecture armel
RUN dpkg --add-architecture armhf
RUN dpkg --add-architecture arm64
RUN apt update
RUN apt install -y libusb-dev:arm64
RUN apt install -y libusb-1.0-0:arm64
RUN apt install -y libusb-1.0-0-dev:arm64
RUN apt install -y libusb-dev:armhf
RUN apt install -y libusb-1.0-0:armhf
RUN apt install -y libusb-1.0-0-dev:armhf
RUN apt install -y linux-libc-dev:armel
RUN apt install -y libusb-dev:armel
RUN apt install -y libusb-1.0-0:armel
RUN apt install -y libusb-1.0-0-dev:armel
# 


ADD ./libusb-macos_10.7 /libusb-macos_10.7
ADD ./libusb-apple-m1 /libusb-apple-m1
ADD ./libusb-MinGW-x64 /libusb-MinGW-x64

ENTRYPOINT ["/build.sh"]
