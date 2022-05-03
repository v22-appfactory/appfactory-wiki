The docker containers can be remotely debugged by launching the application using a remote debugging switch and then
connecting to the listener using the port specified.  This has been done for the services application when it is 
started in the DEV mode.

### Starting the container using the debug switch
#### Container 
* Services Docker file - In the server/Dockerfile there is an ENTRYPOINT that launches the 'dev' task in the project
```javascript
# development server that will restart after changes
ENTRYPOINT  ["npm", "run", "dev"]
```
* Services Compose YML file - The services.yml has a ports setting for redirecting from the host:9229 to the container 
9229 port
```javascript
    ports:
      - 3000:3000
      - 9229:9229
``` 
#### Services Project
 The 'dev' task sets the '--inspect' switch specifying the port as 9229
```javascript
"dev": "nodemon --inspect=0.0.0.0:9229 src/index.js --exec \"node -r dotenv/config -r @babel/register\"",
```
NOTE: When debugging a docker container it is import to specify the '0.0.0.0' host in order to not use localhost which
would be specific to the container as localhost

#### IDE Remote Debugging Configuration
The Webstorm IDE was used to connect remotely and perform the debugging.  A similar facility is probably available in
other development IDEs.  Key settings:   
* Host - localhost
* Port - same as the port specified in the container and project task settings : 9229
* Attach to - Node > 6.3 using '--inspect'
* Reconnect automatically - checked

[[/images/docker/remote-debugging-config.png|Webstorm Remote Debugging Configuration]]
