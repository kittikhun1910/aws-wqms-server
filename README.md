# aws-wqms-server
This is AWS server for IoT project 

``` step1 ```
bulid file docker-compose.yml ``` nano docker-compose.yaml```
``` version: "3.7"

services:
  mosquitto:
    image: eclipse-mosquitto
    hostname: mosquitto
    container_name: mosquitto
    restart: unless-stopped
    ports:
      - "1883:1883"
      - "9001:9001"
    volumes:
      - ./mosquitto:/etc/mosquitto
      - ./mosquitto/mosquitto.conf:/mosquitto/config/mosquitto.conf
```

