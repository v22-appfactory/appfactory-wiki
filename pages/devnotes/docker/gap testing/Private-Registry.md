A Private Registry would provide the ability to house image repositories behind a firewall servicing multiple Docker
instances.  This would provide the storage for both third party image dependencies and multiple versions of project
artifacts.

Testing was done to determine what steps were needed in order to use a private registry.  The following are notes 
related to this work.  The testing was done on a MacOS.


### Installing a Private Registry
The following docker command was used to install the registry container.  The --restart=always will relaunch the
registry each time docker is started or restarted.
``` javascript  
docker run -d -p 5000:5000 --restart=always --name registry registry:2 
```
The registry was added to the Mac Docker Preferences in the insecure registry list;
[[/images/docker/private-registry-on-mac.png|Mac Docker Preferences]]   


### Pushing an Image to the Private Registry
The following steps pull an image from Dockhub and push it to the private registry:
``` javascript
docker pull node
docker tag node:latest localhost:5000/node
docker push localhost:5000/node
```
It is important to note the 'localhost:5000' preface which is necessary to target the private registry running on the
localhost on port 5000.  When using the images the 'localhost:5000' preface was used to reference the images.  The
docker-compose.yml:
``` javascript
version: '3'

services:
  app1:
    build: application
    image: localhost:5000/load-balanced-app
    container_name: app1
    environment:
      MESSAGE: 'First Instance'
    networks:
      static-network:
        ipv4_address: 172.20.0.2
    ports:
      - 8081:8080
  app2:
    build: application
    image: localhost:5000/load-balanced-app
    container_name: app2
    environment:
      MESSAGE: 'Second Instance'
    networks:
      static-network:
        ipv4_address: 172.20.0.3
    ports:
      - 8082:8080
  nginx:
    build: .
    image: localhost:5000/load-balance-nginx
    container_name: nginx
    networks:
      static-network:
        ipv4_address: 172.20.0.4
    ports:
      - 8080:80

networks:
  static-network:
    ipam:
      config:
        - subnet: 172.20.0.0/16
```



