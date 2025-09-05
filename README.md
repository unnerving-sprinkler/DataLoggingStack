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

Copy the token and paste it into .env file under *INFLUXDB_TOKEN=* (No Quotes Needed)

## 3) Setup Cloudflare Access (If Using)
Configure a tunnel in cloudflare zero trust and apply a security application if needed, copy the token for the zero trust tunnel and past it into the .env file. 

Cloudflare Setup:

<img width="574" height="131" alt="image" src="https://github.com/user-attachments/assets/3a38d88c-f7a4-49d1-9f42-aca6317b0344" />


**If running locally and not using cloudflare to access you must uncomment the following lines in docker-compose.yml**
```sh
ports: # Not Exposed to the Public Internet, Access via Cloudflared Tunnel. If Not Using Cloudflared, Uncomment this line to expose the UI on port 8888
  - "8888:80"     
```

## 4) Setup InfluxDB3 Explorer
Navigate to the Explorer webpage, either through the cloudflare link that was setup, or locally localhost:8888

Configure>Servers>New Server
- Provide a friendly name
- Paste your Admin token from the .env file
- Add the route to the influx service: influxdb3-core:8181

## Resources
This guide is based on a guide made by [influx community](https://github.com/InfluxCommunity/TIG-Stack-using-InfluxDB-3/tree/main)

