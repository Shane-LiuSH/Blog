---
date : 2022-08-18
title : 'Deploy MQTT in Docker'
description : 'How to deploy the containers of MQTT and communicate with each other'
slug :
authors : 'Shane'
tags : 
- MQTT
- Docker
categories : 
- Dev 
- Docker
externalLink :
series :
---

# Install the broker_____
## pull the image from the docker hub

`docker pull eclipse-mosquitto`

## download the config file 
* Mount the config file in the container to this file make it easier to config the container.
>https://raw.githubusercontent.com/eclipse/mosquitto/master/mosquitto.conf

## run the container
mount the log file to ram disk with listen port exposed to 8883

`docker run -it --name mqtt_broker -p 8883:1883 -p 9001:9001 -v ~/MQTT/mosquitto.conf:/mosquitto/config/mosquitto.conf -v /mnt/MQTTData:/mosquitto/data -v /mosquitto/log eclipse-mosquitto`

## go inside the container and add the ueser and pwd

`docker exec -it mqtt sh`

`mosquitto_passwd -c /mosquitto/config/pwfile [uesrname]`

`mosquitto_passwd /mosquitto/config/pwfile pwdis123`
************************

# install client

the same as above, change the listening port, the directory hve been createded so you need to mount them

`docker run --name mqtt_client -it -p 8884:1883 -p 9002:9001 -v ~/MQTT/mosquitto.conf:/mosquitto/config/mosquitto.conf -v /mnt/MQTTData:/mosquitto/data -v /mosquitto/log eclipse-mosquitto`

# tweak the ~/MQTT/mosquitto.conf
* if the clients and the broker mount to the same config, you must add the pwdfile first(even it is not necessary to the client and you can just nake an empty file). Otherwise, it may generate errors.
*   uncomment the line: 
    * `password_file` 
    * append ` /mosquitto/config/pwfile`
*   restart the container
    * `docker container restary [name]`

***********************
# Run client
## Go inside the container

`docker exec -it mqtt_client1 sh`

## Subscribe the broker

`mosquitto_sub -h 172.16.18.10 -p 8888 -u pwdis123 -P 123 -t 'test/topic' -v`

## Publish the msg
`mosquitto_pub -h 172.16.18.10 -p 8888 -u pwdis12345 -P 12345 -t 'test/topic' -m 'hello world'`

# Reference
> https://hub.docker.com/_/eclipse-mosquitto
> https://github.com/eclipse/mosquitto
> https://mosquitto.org/man/mosquitto-conf-5.html






