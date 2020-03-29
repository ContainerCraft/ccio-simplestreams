# Build lxd-image-server's Debian package within a container for any platform
#   docker build --tag lxd-image-server-builder --build-arg distro=ubuntu:bionic .
#   mkdir -p dist && docker run --rm lxd-image-server-builder tar -C /dpkg -c . | tar -C dist -xv

ARG distro="ubuntu:bionic"
FROM ${distro}
WORKDIR /root/
ENV \
    LC_ALL=C.UTF-8 \
    LANG=C.UTF-8

ENV apt_FLAGS="\
              -yqq \
              --no-install-recommends \
              -o Dpkg::Options::=--force-unsafe-io \
              "

COPY apt/lxd-image-server_0.0.1_all.deb ./lxd-image-server.deb

RUN set -ex \
 && echo $(pwd) \
 && echo $(ls) \
 && apt-get update -y \
 && echo

RUN set -ex \
 && env DEBIAN_FRONTEND=noninteractive apt-get install ${apt_FLAGS} /root/lxd-image-server.deb \
 && echo

RUN set -ex \
 && apt-get clean \
 && rm -rf "/var/lib/apt/lists"/* \
 && echo

EXPOSE 8080
