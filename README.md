# emotion-docker-services
## Init project
git submodule update --recursive

## Set variables
In `parts_incidencia/.env` set the variables. Focus on the MYSQL password, it must be the one provided in this .env file.

## Build database
docker-compose up -d
DB_HOST=$(docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' gestor-incidencies-mysql)
mysql -h $DB_HOST -uroot -pmy-secret-pw < parts_incidencia/app/model/db_gestor_incidencies.sql

## Deploy servicies
docker-compose up -d

## Show logs
docker-compose logs -f web_server
