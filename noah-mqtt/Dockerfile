ARG BUILD_FROM
FROM $BUILD_FROM
ARG BUILD_FROM
COPY config.json /
RUN apk --no-cache add jq
RUN NOAH_MQTT_VERSION=$(jq --raw-output '.version // empty' config.json) && case "$BUILD_FROM" in \
*"aarch64-base"*) ARCH="arm64";; \
*"armhf-base"*) ARCH="armv6";; \
*"amd64-base"*) ARCH="amd64";; \
esac \
&& curl -L -o /noah-mqtt https://github.com/ma-schmitz/noah-mqtt/releases/download/v0.0.2.4/noah-mqtt && chmod +x /noah-mqtt

COPY rootfs/docker-entrypoint.sh /
RUN chmod a+x /noah-mqtt && chmod a+x /docker-entrypoint.sh
ENTRYPOINT [ "/docker-entrypoint.sh"]
