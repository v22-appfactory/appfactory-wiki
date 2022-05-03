The Keycloak Container provides a Keycloak server that the development environment can authenticate against.  When the
application moves to the test and production the Keycloak server is replaced by a Keycloak server in those environments 
allowing the application containers to utilize the authentication provided there.  

The Keycloak Container is pre-loaded with a realm, client, a role, and users that are expected by the test applications.
Additional users can be added and saved to the AppFactory-realm.json file that will load the AppFactory realm.

## Running Keycloak with Local Projects
While developing the __*appfactory*__ and __*services*__ (appfactory-services) projects the developer runs the Keycloak
container and connects to it by setting the project environment variables
#### Launching the Keycloak Container
The keycloak container can be launched using __*dc-keycloak.sh*__ adding the parameter up/down for lauching/closing:
```javascript
./dc-keycloak.sh up
```
The script launches docker-compose using the __*dc-keycloak.yml*__ file.  Configuration settings of note:
* image: jboss/keycloak - the dockerhub imaage that is being used
* DB_VENDOR: H2 - using default hibernate databases
* KEYCLOAK_USER: admin & KEYCLOAK_PASSWORD:  P@ssw0rd - admin user/password for logging in at 
http://localhost:8081/auth/admin
* KEYCLOAK_IMPORT: /home/AppFactory-realm.json - loads AppFactory realm on startup
* KEYCLOAK_MIGRATION_STRATEGY: OVERWRITE_EXISTING - existing AppFactory settings will be replaced by the import
* Keycloak server is running on port 8081
```javascript
    command:
      -Djboss.socket.binding.port-offset=1
    ports:
      - 8081:8081
```
#### Front-end Connection
The __*appfactory*__ project connects with the Keycloak container using the following environment variables:
VUE_APP_KEYCLOAK_CLIENT=appfactoryClient
VUE_APP_KEYCLOAK_URL=http://localhost:8081/auth
VUE_APP_KEYCLOAK_REALM=AppFactory  
These can either be set as environment variables using the users profile or a .env.local file can be created in the 
project root which will be loaded when the front-end is launched. 
#### Back-end Connection
The __*services*__ project connects with the Keycloak container using the following environment variables:
KEYCLOAK_CLIENT=appfactoryClient
KEYCLOAK_URL=http://localhost:8081/auth
KEYCLOAK_REALM=AppFactory

## Running Keycloak with Project Containers
When running the projects in containers there are a number of steps that are needed to configure the environment and 
launch the containers.  One of the key issues is that the front-end will connect with the Keycloak server from the 
browser (host) using 127.0.0.1:8081 while the back-end will connect on the container network using the DNS name 
__*keycloak*__.  When keycloak validates the token it will compare the two URI values using the front-end URI as a 
source and the back-end URI as the validating value.  The two values must be the same.  The environment variables 
involved are:
VUE_APP_KEYCLOAK_URL=http://localhost:8081/auth
KEYCLOAK_URL=http://localhost:8081/auth
This is complicated when the services container validates the token by making a request to the keycloak container; it 
cannot use 'localhost' and instead needs to use the container network name 'keycloak'.  From the dc-keycloak.yml:
```javascript
services:
  keycloak:
```  
This results in the URI: KEYCLOAK_URL: http://keycloak:8081/auth
Because of the validating comparison described above the front-end URI must match: VUE_APP_KEYCLOAK_URL: 
http://keycloak:8081/auth
#### Solution
Once these environment variables are set in this way it is necessary to add this value to the host file so that on the
host the __*keycloak*__ name is mapped to 127.0.0.1.  In the hosts (/etc/hosts on the Mac) file:
```javascript
127.0.0.1	keycloak
```
It is also necessary for Keycloak to connect on port 8081 both when connecting from the host and inside the container 
network allowing both URIs to specify the port as 8081.  This is done in the keycloak.yml file as described above.
#### Front-end Container Connection
The __*appfactory*__ container connects with the Keycloak container using the following environment variables in 
dc-web.yml:
```javascript
VUE_APP_KEYCLOAK_CLIENT:  appfactoryClient
VUE_APP_KEYCLOAK_URL:     http://keycloak:8081/auth
VUE_APP_KEYCLOAK_REALM:   AppFactory
```
#### Back-end Container Connection
The __*services*__ container connects with the Keycloak container using the following environment variables in 
services.yml:
```javascript
KEYCLOAK_CLIENT:        appfactoryClient
KEYCLOAK_URL:           http://keycloak:8081/auth
KEYCLOAK_REALM:         AppFactory
```
#### Launching the Integrated Development Containers
The integrated development containers can be launched using __*dc-dev-app.sh*__ adding the parameter up/down for 
lauching/closing:
```javascript
./dc-dev-app.sh up
```




