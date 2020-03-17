---
title: "Getting data from CurrentCost to HomeAssistant with rtl_433 and MQTT"
date: 2020-03-15T11:50:00+00:00
draft: false
---

I have had a CurrentCost Power sampling device on my house electrical supply for a few years, since I got it free switching providers. It came with a panel that allows you to view the momentary values for power consumption, but in these days of data aggregation and IoT, this is as close to useless as it gets. I already have a [HomeAssistant](https://www.home-assistant.io) server runniing on a Docker Host I use for such things, and I have a few other IoT-friendly devices lying around, so I thought I would try to integrate these to gather and display historical power consumption for my home.

## Data collection with rtl_433

I have a few [RTLSDR](https://www.rtl-sdr.com) devices, and the CurrentCost unit transmits metrics on 433MHz ISM, so teh first step is to configure a device that will gather this data over RF. Since I plan to use this as a sort of RF gathering hub, I will use a spare Pi3b and one of the RTLSDR devices.

I installed a fresh [Rasbian Buster](https://www.raspberrypi.org/downloads/raspbian/) and configured a static network lease.
Once this was done, I installed _rtl-sdr_ and *rtl_433*, as follows:

     $ sudo apt install rtl-sdr
     $ sudo apt-get install libtool libusb-1.0.0-dev librtlsdr-dev
     $ sudo apt-get install git git-core cmake libusb-1.0-0-dev
     $ git clone https://github.com/merbanan/rtl_433.git
     $ cd rtl_433/ && mkdir build && cd build && cmake ../ && make
     $ sudo make install

## Containerised MQTT
Once I had a working install of *rtl_433*, the next step was to setup an [MQTT](http://mqtt.org) broker to pass messages between the client (rtl_433) and *HomeAssistant*. *HomeAssitant* does have an MQTT broker module, but the Docker install does not include the Supervisor and Add-Ons functionality, so deploying a Containerised solution is more in keeping with the modular ideology that is in vogue today. The Docker host I use for this stuff uses [Docker Compose](https://docs.docker.com/compose/) to manage the deployment and configuration of Docker images, so I added the following to docker-compose.yml:

    # Mosquitto - MQTT Broker
      mosquitto:
        image: eclipse-mosquitto
        hostname: mosquitto
        container_name: mosquitto
        expose:
          - "1883"
          - "9001"
        ports:
          - "1883:1883"
          - "9001:9001"
        volumes:
          - ${USERDIR}/docker/mosquitto/config:/mosquitto/config
          - ${USERDIR}/docker/mosquitto/logs:/mosquitto/logs
          - ${USERDIR}/docker/mosquitto/data:/mosquitto/data
        networks:
          - default

I then brought the container up with `docker-compose up -d` and my MQTT broker was active.
The next step was to configure *HomeAssitant* to listen to the MQTT broker for messages. This is done by entering the Configuration section, and selecting Integrations and clicking the orange + to add an integration. Find MQTT, and enable. Then enter the details for the MQTT broker and it's all done. Well almost...

## Configuring HomeAssistant
The nest step is to configure *HomeAssistant* to listen for a Topic and to make data from this topic avaialble as a variable for use in the UI. The following snippet should be added to `configuration.yml`:

    sensor:
      - platform: mqtt
        state_topic: "CurrentCost/Power/power0_W"
        name: "CurrentCost_Power"
        unit_of_measurement: "Wh"
        device_class: power

This listens for anything posted on the Topic `CurrentCost/Power/power0_W`, and assigns it the variable name *CurrentCost\_Power*. It also assigns a device class of 'power' so that HomeAssistant will know what icons to use for the variable. Where does this Topic come from? The configuration of *rtl\_433* comes next.

## Configuring rtl_433 to post Topics
*rtl\_433* can output data it reads in many formats. The default is as a formatted table to stdout, i.e. the screen. However, for our purposes, the pretty-formatting is superfluous. It can also do JSON, CSV and other machine-readable formats, and, of most interest to us, it can connect directly to an MQTT broker and post Topics. To do this, we create a configuration file for *rtl\_433*. If a file is created in one of a few specific locations, *rtl\_433* will automatically load it and use it to configure itself. In this instance, we will create the file at `/etc/rtl_433/rtl_433.cfg`

    frequency     433.92M
    report_meta time:iso
    report_meta protocol
    output mqtt://192.168.1.105:1883,retain=0,devices=CurrentCost/Power
    stop_after_successful_events false
    protocol 44  # CurrentCost Current Sensor

This configures *rtl\_433* to listen on 433.920MHz ISM band for Protocol 25 devices (CC Sensor) and output the data to an MQTT broker using the Topic` CurrentCost/Powe`r. It will send multiple parameters, which can be seen by using Developer Tools -> MQTT in HomeAssistant and selecting the Topic CurrentCost/Power/#, but `power0_W` is the one we are interested in.

Once we have *rtl\_433* configured, we configure systemd to maintain it, as follows - create a Unit file in `/etc/systemd/system/rtl_433-mqtt.service`

    [Unit]
    Description=rtl_433 to MQTT publisher
    After=network.target
    [Service]
    ExecStart=/usr/local/bin/rtl_433
    Restart=always
    RestartSec=5
    [Install]
    WantedBy=multi-user.target

Once created, we can start & enable the service as follows:

    $ sudo systemctl enable rtl_433-mqtt.service
    $ sudo systemctl start rtl_433-mqtt.service




