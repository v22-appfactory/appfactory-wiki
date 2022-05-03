## Test Application
A test application was pulled from the Internet and updated to provide a sample application that uses both Node and 
Nginx.  The test application consisting of an nginx container and a web app container.  When running there is a single
nginx instance and two web app instances.  The nginx endpoint load balances between the two webapp instances (one 
displays 'First Instance' and the other 'Second Instance').    
The Nginx container is built using a third party Nginx and providing a nginx configuration file.  The Dockerfile:
``` javascript
FROM localhost:5000/nginx

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d/default.conf 
``` 
Default.conf:
``` javascript
upstream my-app {
  least_conn;
  server 172.17.0.1:8081 weight=1;
  server 172.17.0.1:8082 weight=1;
}

server {
  listen 80;

  location / {
    proxy_pass     http://my-app;
    proxy_redirect off;
  }
}
```   
The webapp uses a third party Node container creating a website with a simple index.js file.  The Dockerfile: 
``` javascript
FROM localhost:5000/node
RUN mkdir -p /usr/src/app
COPY index.js /usr/src/app
EXPOSE 8080
CMD ["node", "/usr/src/app/index"]
```  
The index.js file:
``` javascript
var http = require('http');
var fs = require('fs');

http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.end(`<h1>${process.env.MESSAGE}</h1>`);
}).listen(8080);
``` 
The application is launched using a docker compose file (docker-compose.yml) which launches the following instances 
and sets up the network and IP addresses.  The compose file launches three services:
* App1 - instance of the web app with the message 'First Instance', running on 172.20.0.2 sending host port 8081 
requests to the container's 8080 port.
* App2 - instance of the web app with the message 'Second Instance', running on 172.20.0.3 sending host port 8082 
requests to the container's 8080 port.
* Nginx - instance of the nginx container that acts as a router sending host 8080 requests to port 80 and
load-balancing requests between the two web app instances.

Repeated calls to localhost:8080 should switch between the two web application pages showing the following:    
[[/images/apps/sample app/first-instance.png|First Instance]]   
[[/images/apps/sample app/second-instance.png|Second Instance]]   

The files for this application are in the appfactory-docker repo: https://github.com/gmarshall142/appfactory-docker
in the 'nginx' directory.    
To start: CD into the nginx directory and enter _'docker-compose up'_ on the commandline   
To stop:  CD into the __nginx__ directory and enter _'docker-compose down'_ on the commandline
