# Documentation
A simple docker compose file to run a mongodb database in docker with replica set on.

## Requirements
* Install [Docker]('https://www.docker.com/products/docker-desktop') and [docker compose]('https://docs.docker.com/compose/install/') if you don't have them already.

## Installation
1. Clone the repository:
```bash
git clone https://github.com/javilobo8/mongors.git && cd mongors
```
2. Copy default configuration to .env file:
```bash
cp .env.example .env
```
3. Apply the configuration you want to the .env file:
  - `RS` -> The replicas set name (Default: rs0)
  - `HOST` -> The replica set host (Default: 127.0.0.1)
  - `PORT` -> The replica set port (Default: 27017)
  - `DATA` -> The folder where the database information will be stored (Default: ./data/db)
4. Start the container
```bash
docker compose up -d
```
5. Initialize the replica set (Only the first time you run the container)
```bash
docker exec -it rs0 mongosh # This will open the mongo shell
rs.initiate() # This will initialize the replica set
rs.status() # This will show the replica set status
exit # This will exit the mongo shell
```

## Updating from previous versions
If you are updating from a previous version, you will need to remove the old container and create a new one. To do so, follow these steps:
1. Stop the container
```bash
docker compose down
```
2. Remove the container
```bash
docker rm rs0
```
3. Check mongodb version in `compose.yml` file and update it if needed
4. Start the container
```bash
docker compose up -d
```
