ARG BUILD_FROM=hassioaddons/base-amd64:1.0.1
FROM ${BUILD_FROM}

# Copy root filesystem
COPY rootfs /

# Setup base
RUN \
    apk add --no-cache \
        --repository http://nl.alpinelinux.org/alpine/edge/main \
        libuv \
    \
    && apk add --no-cache \
        --repository http://dl-cdn.alpinelinux.org/alpine/edge/community \
        nodejs-current \
        nodejs-current-npm \
    \
    && apk add --no-cache --virtual .build-dependencies \
        avahi-dev \
        g++ \
        libffi-dev \
        make \
        openssl-dev \
        python \
    \
    && apk add --no-cache \
        avahi \
        avahi-compat-libdns_sd \
        dbus \
        git \
    \
    && npm set unsafe-perm true \
    \
    && npm -g install \
        node-gyp \
        homebridge@0.4.33 \
        homebridge-homeassistant@3.0.2 \
    \
    && apk del --purge .build-dependencies

CMD [ "/usr/bin/run.sh" ]

# Build arugments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Homebridge" \
    io.hass.description="HomeKit support for your Home Assistant instance using Homebridge" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Franck Nijhof <frenck@addons.community>" \
    org.label-schema.description="HomeKit support for your Home Assistant instance using Homebridge" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="Homebridge" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://addons.community" \
    org.label-schema.usage="https://github.com/hassio-addons/addon-homebridge/tree/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/hassio-addons/addon-homebridge" \
    org.label-schema.vendor="Community Hass.io Add-ons"
