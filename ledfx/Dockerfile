ARG BUILD_FROM=hassioaddons/base-python:5.1.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Copy Python requirements file
COPY requirements.txt /tmp/

# Setup base
ARG BUILD_ARCH=amd64
RUN \
    apk add --no-cache --virtual .build-dependencies \
        build-base \
        cython \
        g++ \
        gcc \
        gfortran \
    && apk add --no-cache \
        alsa-plugins-pulse \
        lua-resty-http \
        nginx \
        nginx-mod-http-lua \
        portaudio-dev \
    && pip3 install \
        --no-cache-dir -r /tmp/requirements.txt \
    && rm -fr \
        /tmp/* \
        /etc/nginx \
    && apk del --no-cache --purge .build-dependencies

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="ledfx" \
    io.hass.description="Network based LED effect controller" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="phixion <just@for.testing>" \
    org.label-schema.description="Network based LED effect controller" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="ledfx" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://community.home-assistant.io/?u=phixion" \
    org.label-schema.usage="https://github.com/phixion/addon-ledfx/blob/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/phixion/addon-ledfx" \
    org.label-schema.vendor="Community Home Assistant Addons"
