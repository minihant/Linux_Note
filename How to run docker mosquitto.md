# How to run docker eclipse-mosquitto
[reference](https://hub.docker.com/_/eclipse-mosquitto/)


## RUN
   ```
   $ sudo sudo mkdir -p /mosquitto/{config,data,log}
   EX:
	$ sudo docker run -it -p 1883:1883 -p 9001:9001 -v mosquitto.conf:/mosquitto/config/mosquitto.conf --name mqtt eclipse-mosquitto
   ```

## run mqtt & node-red docker
   1. run mqtt
   ```
   $ sudo docker run -it -p 1883:1883 -p 9001:9001 --name mqtt eclipse-mosquitto
   ```
   2. run node-red
   ```
   $ sudo docker run -p 1880:1880 --name m3 hant/nodered
   ```
