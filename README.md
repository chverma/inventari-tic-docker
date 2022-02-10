# Docker infraestructure for inventari-tic
## Init project
git submodule init

git submodule update --recursive

## Copy env file
cp {,.}env

cp inventari-tic/{,.}env
## Set variables
In `inventari-tic/.env` set the variables. Focus on the MYSQL password, it must be the one provided in this .env file.

# Install npm packages
(cd inventari-tic && npm i)
## Build database
docker-compose up -d && \
DB_HOST=$(docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' inventari-tic-mysql) &&
mysql -h $DB_HOST -uroot -pmy-secret-pw < inventari-tic/app/model/db_inventari_tic.sql

## Deploy servicies
docker-compose up -d

## Show logs
docker-compose logs -f web_server
