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





ADD ./libusb-macos_10.7 /libusb-macos_10.7
ADD ./libusb-apple-m1 /libusb-apple-m1
ADD ./libusb-MinGW-x64 /libusb-MinGW-x64


# Extra

RUN apt update
RUN apt update
RUN apt install -y libatlas-base-dev libblas-dev liblapack-dev

ENTRYPOINT ["/build.sh"]
