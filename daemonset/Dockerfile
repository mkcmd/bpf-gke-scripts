###
# Extract cmd binary from deb package
#
# The Cmd daemonset only requires the cmd binary from the installer package.
# This stage extracts the binary from a .deb file, so it can be copied into the daemonset image.
###
FROM ubuntu:bionic as extractor

ARG CMD_VERSION

RUN apt update \
    && apt install --no-install-recommends -y binutils tar \
    && apt clean

WORKDIR /tmp/cmd

COPY cmd-*.amd64.deb cmd.deb

RUN ar x cmd.deb \
    && tar -xf data.tar.gz



###
# Daemonset image
###
FROM ubuntu:bionic

RUN apt update \
    && apt install --no-install-recommends -y ca-certificates libcap2 libelf1 curl \
    && apt clean

COPY --from=extractor /tmp/cmd/sbin/cmd /sbin/cmd

CMD ["/sbin/cmd", "-f"]
