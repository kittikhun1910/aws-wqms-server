# aws-wqms-server
This is AWS server for IoT project 

``` step1 ```
bulid file docker-compose.yml ``` nano docker-compose.yaml ```
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

```   influxdb:
    image: influxdb:latest
    container_name: influxdb
    ports:
      - "8086:8086"
    networks:
      - iot
    volumes:
      - ./influxdb/data:/var/lib/influxdb2
      - ./influxdb/config:/etc/influxdb2
    environment:
      - DOCKER_INFLUXDB_INIT_MODE=setup
      - DOCKER_INFLUXDB_INIT_USERNAME=user001
      - DOCKER_INFLUXDB_INIT_PASSWORD=passwd001
      - DOCKER_INFLUXDB_INIT_ORG=my-org
      - DOCKER_INFLUXDB_INIT_BUCKET=my-bucket
      - DOCKER_INFLUXDB_INIT_ADMIN_TOKEN=my-token
```

```   telegraf:
    image: telegraf:latest
    container_name: telegraf
    volumes:
      - ./telegraf/telegraf.conf:/etc/telegraf/telegraf.conf:ro
    depends_on:
      - mosquitto
      - influxdb
    networks:
      - iot

```

``` step2 ``` config file mosquotto.pw, mosquitto.conf ,telegraf.conf for your data
- ``` step3``` run command in teminal for start dockerfile
``` docker-compose up -d ```
