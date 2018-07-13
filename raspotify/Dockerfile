ARG BUILD_FROM=debian:jessie
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

RUN apt-get update
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
