

## Running load tasks script
The *tpdr-loadtask.sh* loads Task records from a DSV dump.  Currently it is set to only load the first 250 records.  It
is run from the services container which uses the environment variable __POSTGRES_SERVER__ to set the Sequelize server.
``` javascript
docker exec -it appserver /bin/bash
cd /usr/src/app/scripts
export POSTGRES_SERVER=postgres
./tpdr-loadtask.sh
```



## Dump Database
There is a volume share at /usr/volumes that can be used for dumping from the Postgres container to the host.
``` javascript
docker exec -it postgres /bin/bash
pg_dump -U postgres appfactory > /usr/volumes/postgres/appfactory-100520.sql
```
This SQL file can then be used for saving any records.


## Issues using the appfactory source code.
Issue were encountered when launching the web container that have to do with executing the vue-cli in that container.
When running 'npm run serve' to launch the web application errors were thrown because the 
node_modules/.bin/vue-cli-service was not created correctly.  Normally this is a link file to the 
../@vue/cli-service/bin/vue-cli-service.js.  In order to correct this it was necessary to take the following steps:
* On the host remove the node_modules directory and package-lock.json file using the Git Bash terminal 
``` javascript
cd /c/tpdr/workspace/app-factory/appfactory directory
rm -rf node_modules
rm package-lock.json
```
* Recreate the node_modules directory on the web container    
##### Host
  * Modify the web Dockerfile to not launch the app but keep the container open
    * In file explorer open the file c:\tpdr\workspace\app-factory\appfactory-docker\web\Dockerfile
    * comment the line: CMD ["npm", "run", "serve"]
    * uncomment or enter the line: CMD tail -f /dev/null
  * Clear the web image so that it will be rebuilt with the modified Dockerfile
  ```javascript 
  docker image rm appfactory-web 
  ```
  * Restart the servers and enter the __web__ container:
```javascript
./dc-win-app.sh up
docker exec -it web /bin/bash  
```
  * Run npm install 
```javascript
cd /usr/src/web
npm install
```
* Restart the containers launching the application on the web container
  * Stop the running containers and close them: Ctrl-C and run __./dc-win-app.sh down__
  * Modify the web Dockerfile to launch the app but keep the container open
    * In file explorer open the file c:\tpdr\workspace\app-factory\appfactory-docker\web\Dockerfile
    * uncomment the line: CMD ["npm", "run", "serve"]
    * comment the line: CMD tail -f /dev/null
  * Clear the web image so that it will be rebuilt with the modified Dockerfile
  ```javascript 
  docker image rm appfactory-web 
  ```
  * Restart the servers:
```javascript
./dc-win-app.sh up
```
