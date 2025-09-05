# Data Monitoring Stack
Use this template to stand-up a monitoring stack || In my case I am using it on a Digital Ocean instance

## Setup 
Make sure that you have Docker installed on your system, some familularity with docker compose is needed [Docker Install Guide](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository).

Tested on Ubuntu 25.04 in Digital Ocean cloud

## 1) Clone Repo
Download the repo to your home folder and move into folder
```sh
git clone https://github.com/unnerving-sprinkler/DataLoggingStack.git
cd DataLoggingStack
```

## 2) Start Just InfluxDB
Start just the InfluxDB Instance and generate a ADMIN token, this is a new step that is needed in Influx3Core
```sh
docker compose up -d influxdb3-core
docker compose exec influxdb3-core influxdb3 create token --admin
```

Copy the token and paste it into the .env file under *INFLUXDB_TOKEN=* (No Quotes Needed)

## Resources
This guide is based on a guide made by [influx community](https://github.com/InfluxCommunity/TIG-Stack-using-InfluxDB-3/tree/main)

