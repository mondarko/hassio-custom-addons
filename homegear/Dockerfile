ARG BUILD_FROM=hassioaddons/debian-base-amd64
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

RUN apt-get update && apt-get -y install apt-transport-https wget ca-certificates apt-utils gnupg libzip4 libavahi-client3 libavahi-client-dev insserv
RUN wget https://apt.homegear.eu/Release.key && apt-key add Release.key && rm Release.key
RUN echo 'deb https://apt.homegear.eu/Raspbian/ stretch/' >> /etc/apt/sources.list.d/homegear.list
RUN apt-get update && apt-get -y install ntp tzdata homegear homegear-management homegear-webssh homegear-adminui homegear-nodes-core homegear-nodes-extra homegear-homematicbidcos homegear-influxdb vim less htop
RUN rm -f /etc/homegear/dh1024.pem
RUN rm -f /etc/homegear/homegear.crt
RUN rm -f /etc/homegear/homegear.key
RUN cp -R /etc/homegear /etc/homegear.config
RUN cp -R /var/lib/homegear /var/lib/homegear.data

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY start.sh /start.sh
RUN chmod +x /start.sh
CMD /start.sh

EXPOSE 2001 2002 2003

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Homegear" \
    io.hass.description="Homegear for Homematic devices Hass.io add-on" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="mondarko" \
    org.label-schema.description="Homegear for Homematic devices Hass.io add-on" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="Homegear" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://github.com/mondarko" \
    org.label-schema.usage="https://github.com/mondarko/hassio-custom-addons" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/mondarko/hassio-custom-addons" \
    org.label-schema.vendor="mondarko"
