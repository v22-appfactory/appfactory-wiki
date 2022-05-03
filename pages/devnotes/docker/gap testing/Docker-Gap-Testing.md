# Overview
In order to run Docker behind a firewall it will be necessary to have a plan for getting both third party and project
container images onto the Docker server.  The following is a short discussion of some of the testing that was done
while determining the requirements for deploying to a Docker server.

The 'air gap' testing consisted of the following:

* [Docker Gap Testing Test Application](Gap-Testing-Testapp "Docker Gap Testing Test Application")  
Nginx test application consisting of an nginx container and a web app container.  
* [Private Registry](Private-Registry "Private Registry")  
A private docker registry provides image repositories for the container images used by the docker site.
* Saved the images to TAR files and then reloaded them into Docker using the docker commands (save/load).  See below.
* Tested running the Docker application with no Internet connection in order to prevent access to dockerHub and simulate
running behind a firewall.  The application was started from a YAML file using docker-compose.



## Save / Load Images
Once the container images are created they can be saved to a TAR file, moved to the isolated network, and loaded into
Docker using the Load command.  There were four images in the test application:
* node
* nginx
* load-balanced-app - used node image
* load-balance-nginx - used nginx image

The following commands were used to save and load the images:
``` javascript
# saving images to a tar archive
docker image save -o ~/docker/images/node.tar localhost:5000/node
docker image save -o ~/docker/images/nginx.tar localhost:5000/nginx
docker image save -o ~/docker/images/load-balanced-app.tar localhost:5000/load-balanced-app
docker image save -o ~/docker/images/load-balance-nginx.tar localhost:5000/load-balance-nginx

# loading an image
docker image load -i ~/docker/images/node.tar
docker image load -i ~/docker/images/nginx.tar
docker image load -i ~/docker/images/load-balanced-app.tar
docker image load -i ~/docker/images/load-balance-nginx.tar
```

The following shows the session where the images were first cleared, then loaded from the TAR files, then the local 
images were reviewed. 
 
``` javascript
$ docker images -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

$ docker image load -i ~/docker/images/node.tar

97041f29baff: Loading layer [==================================================>]  105.6MB/105.6MB
2f77733e9824: Loading layer [==================================================>]   24.1MB/24.1MB
687890749166: Loading layer [==================================================>]  8.005MB/8.005MB
b8f8aeff56a8: Loading layer [==================================================>]  146.4MB/146.4MB
a72a7e555fe1: Loading layer [==================================================>]  575.9MB/575.9MB
799e7111d6d4: Loading layer [==================================================>]  349.2kB/349.2kB
1af9673a387c: Loading layer [==================================================>]   96.1MB/96.1MB
bf47ba7444d6: Loading layer [==================================================>]  5.496MB/5.496MB
d0df4aee8f88: Loading layer [==================================================>]  3.584kB/3.584kB
Loaded image: localhost:5000/node:latest
~/workspace/app-factory/appfactory-docker/nginx (master) $ 
~/workspace/app-factory/appfactory-docker/nginx (master) $ docker image load -i ~/docker/images/nginx.tar
b67d19e65ef6: Loading layer [==================================================>]   72.5MB/72.5MB
6eaad811af02: Loading layer [==================================================>]  57.54MB/57.54MB
a89b8f05da3a: Loading layer [==================================================>]  3.584kB/3.584kB
Loaded image: localhost:5000/nginx:latest
~/workspace/app-factory/appfactory-docker/nginx (master) $ docker image load -i ~/docker/images/load-balanced-app.tar
403b2e5e8e2c: Loading layer [==================================================>]   2.56kB/2.56kB
85a760e49a9d: Loading layer [==================================================>]  3.584kB/3.584kB
Loaded image: localhost:5000/load-balanced-app:latest
~/workspace/app-factory/appfactory-docker/nginx (master) $ docker image load -i ~/docker/images/load-balance-nginx.tar
2c54c8a45215: Loading layer [==================================================>]  3.072kB/3.072kB
330115705509: Loading layer [==================================================>]  3.584kB/3.584kB
Loaded image: localhost:5000/load-balance-nginx:latest

~/workspace/app-factory/appfactory-docker/nginx (master) $ docker images -a
REPOSITORY                          TAG                 IMAGE ID            CREATED             SIZE
localhost:5000/load-balance-nginx   latest              4f4be3a2124f        18 hours ago        126MB
localhost:5000/load-balanced-app    latest              40ebe759e9ae        18 hours ago        933MB
localhost:5000/node                 latest              4ac0e1872789        6 days ago          933MB
localhost:5000/nginx                latest              540a289bab6c        7 days ago          126MB
```   
__NOTE:__ The 'localhost:5000' preface for the images resulted from experiments 'pushing' the images to a private
repository and were not necessary for the save/load operation.
 
## Running the application
The files for this application are in the appfactory-docker repo: https://github.com/gmarshall142/appfactory-docker  
The relevant files are in the 'nginx' directory.   
   
To start: CD into the nginx directory and enter _'docker-compose up'_ on the commandline   
To stop:  CD into the __nginx__ directory and enter _'docker-compose down'_ on the commandline
