ARG BUILD_FROM=hassioaddons/base:2.0.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Setup base
RUN apk add --no-cache \
    coreutils=8.29-r2 \
    wget=1.19.5-r0

RUN curl -sL https://dtcooper.github.io/raspotify/install.sh | sh

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
