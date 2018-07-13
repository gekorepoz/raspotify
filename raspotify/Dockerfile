ARG BUILD_FROM=debian:jessie
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Environment variables
ENV \
    DEBIAN_FRONTEND="noninteractive" \
    HOME="/root" \
    LANG="C.UTF-8" \
    PS1="$(whoami)@$(hostname):$(pwd)$ " \
    S6_BEHAVIOUR_IF_STAGE2_FAILS=2 \
    S6_CMD_WAIT_FOR_SERVICES=1 \
    TERM="xterm"

# Install base system
ARG BUILD_ARCH=amd64
RUN apt-get update
RUN apt-get install -y --no-install-recommends \
        bash \
        ca-certificates \
        curl \
        jq \
        tzdata \
    \
    && if [ "${BUILD_ARCH}" = "i386" ]; then S6_ARCH="x86"; else S6_ARCH="${BUILD_ARCH}"; fi \
    \
    && curl -L -s "https://github.com/just-containers/s6-overlay/releases/download/v1.21.4.0/s6-overlay-${S6_ARCH}.tar.gz" \
        | tar zxvf - -C / \
    \
    && mkdir -p /etc/fix-attrs.d \
    && mkdir -p /etc/services.d \
    \
    && \
        if [ "${BUILD_ARCH}" != "armhf" ]; then \
            rm -f /usr/bin/qemu-arm-static; \
        fi \
    \
    && \
        if [ "${BUILD_ARCH}" != "aarch64" ]; then \
            rm -f /usr/bin/qemu-aarch64-static; \
        fi \
    \
    && rm -f -r /tmp/* \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/* \
    && rm -rf /var/{cache,log}/*

RUN apt-get install curl apt-transport-https gnupg2 ca-certificates -y --no-install-recommends

ENV SOURCE_REPO="deb https://dtcooper.github.io/raspotify jessie main"

ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=true
RUN curl -sSL https://dtcooper.github.io/raspotify/key.asc | apt-key add -v -

RUN echo "$SOURCE_REPO" | tee /etc/apt/sources.list.d/raspotify.list

RUN apt-get update
RUN apt-get -y install raspotify

# Build arugments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Raspotify" \
    io.hass.description="Raspotify by https://github.com/dtcooper/raspotify" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Iacami Gevaerd <iacamigevaerd@gmail.com>" \
    org.label-schema.description="Raspotify - Spotify Connect client for the Raspberry Pi that Just Works™" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="Raspotify" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://addons.community" \
    org.label-schema.usage="https://github.com/dtcooper/raspotify/tree/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/dtcooper/raspotify" \
    org.label-schema.vendor="https://github.com/dtcooper/raspotify"
