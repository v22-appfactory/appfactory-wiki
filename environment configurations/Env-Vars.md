# Environment Variables
Environment variables are used to configure the database connection variables, volume locations, Keycloak connection 
parameters, and other variables such as URLs used by the application.  The environment variables are set using a 
combination of OS environment variables on the machine and .env files.  It is important to keep configuration variables
out of the version control.  This document outlines what environment variables are used by each part of the application
and where these are set.
   
## Local Host
The following environmental variables need to be set on the local machine for various functions described below.

The path variables are needed both for running locally and for use by the docker containers.  They are specific to the
location of the application data and the source code on the local machine:
```javascript
APPFACTORY_VOLUME_PATH=/path/to/docker/volumes
APPFACTORY_SOURCE_PATH=/path/to/root/of/source/project/directories
```
These values need to be set for use in the script to load TPDR tasks:
```javascript
POSTGRES_NAME=appfactory
POSTGRES_USER=appuser
POSTGRES_PSWD=*******
POSTGRES_SERVER=localhost
```

The postgres password is need by both the TPDR script above and when building the application for the PROD docker
container:
```javascript
POSTGRES_PSWD=*******
```
## Appfactory project (UI)
Running the Vue / UI project uses a .env.local file in the root of the project with the following variables:
```javascript
VUE_APP_LEVEL=debug
VUE_APP_MODE=DEV

APPFACTORY_VOLUME_PATH=/path/to/docker/volumes
APPFACTORY_SOURCE_PATH=/path/to/root/of/source/project/directories

POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_NAME=appfactory
POSTGRES_USER=appuser
POSTGRES_PSWD=*******
POSTGRES_OWNER=appowner
POSTGRES_OWNER_PSWD=V-22specialProjects

VUE_APP_PROTOCOL=http
VUE_APP_REST_HOST=localhost
VUE_APP_REST_PORT=3000
VUE_APP_WEB_HOST=localhost
VUE_APP_WEB_PORT=8080

VUE_APP_KEYCLOAK_CLIENT=appfactoryClient
VUE_APP_KEYCLOAK_URL=http://localhost:8081/auth
VUE_APP_KEYCLOAK_REALM=AppFactory
VUE_APP_KEYCLOAK_SECRET=V-22specialProjects
```

## Services project (REST API)
Running the services / REST project uses a .env file in the root of the project with the following variables:
```javascript
VUE_APP_LEVEL=debug
VUE_APP_MODE=DEV

APPFACTORY_VOLUME_PATH=/path/to/docker/volumes

POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_NAME=appfactory
POSTGRES_USER=appuser
POSTGRES_PSWD=*******
POSTGRES_OWNER=appowner
POSTGRES_OWNER_PSWD=V-22specialProjects
POSTGRES_MAX_RESULT=1000

VUE_APP_PROTOCOL=http
VUE_APP_REST_HOST=localhost
VUE_APP_REST_PORT=3000

KEYCLOAK_CLIENT=appfactoryClient
KEYCLOAK_URL=http://localhost:8081/auth
KEYCLOAK_REALM=AppFactory
KEYCLOAK_SECRET=V-22specialProjects
```
## Docker
The different docker containers make use of .env files that are specified in the start scripts.         
### Keycloak
./keycloak/.env.keycloak
### DEV
./dev/.env.dev
### PROD
./prod/.env.prod
### NGINX
./nginx/.env.http
