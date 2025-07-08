FROM ghcr.io/home-assistant/amd64-base:3.20 
# Using Alpine 3.20 base image for stability

# Define environment variables
# ... (rest of your ENV block unchanged) ...

LABEL Maintainer="skipnyip" \
Description="This image is used to start the RTL433 to HASS script that will monitor for 433Mhz devices and send the data to an MQTT server"

WORKDIR /data

# Copy scripts
COPY entry.sh rtl_433_mqtt_hass.py /scripts/
# install rtl_433, rtl-sdr, libusb, mosquitto-clients, python3 py3-paho-mqtt; and deps of rtl_433_mqtt_hass.py.
# make entry.sh and rtl_433_mqtt_hass.py executable.
RUN echo "https://nl.alpinelinux.org/alpine/v3.20/main" > /etc/apk/repositories && \
    echo "https://nl.alpinelinux.org/alpine/v3.20/community" >> /etc/apk/repositories && \
    apk update --quiet && \
    apk upgrade && \
    apk add --no-cache --verbose rtl-sdr rtl_433 libusb mosquitto-clients python3 py3-paho-mqtt && \
    chmod +x /scripts/entry.sh && \
    chmod +x /scripts/rtl_433_mqtt_hass.py

# Execute entry script
ENTRYPOINT [ "/scripts/entry.sh" ]
