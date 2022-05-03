The following is a summary of the steps needed to setup a Windows Server with Postgresql, the services application, and
the web application.  Further details can be found on the referenced pages.

1. Software Downloads and Installations   
  1a. NPM/Node  
  1b. Git (if working with repositories directly on the server)  
  1c. IIS     
  1d. IIS Rewrite plugin  
  1e. Postgresql (newest version available; version 10 or greater)  
  1f. PM2    
  
2. Source Repositories  
Either the cloned source repositories or a production version of the applications will be needed on the server.   
  2a. Services - https://github.com/gmarshall142/appfactory-services.git   
  NOTE: This repository also contains the SQL scripts for loading sample data for test and demo  
  2b. Web - https://github.com/gmarshall142/appfactory.git   
  2c. Migrations (used for loading the initial database) - https://github.com/gmarshall142/appfactory-migrations.git
   
3. POSTGRES Database
The setup of the postgres database is covered in the detail page: 
[Postgresql on Windows](Postgresql-Windows "Postgresql on Windows")

4. IIS  
* Two IIS websites were created: Appfactory and Web.  The Appfactory application is used as a reverse-proxy which will 
redirect HTTPS requests to the services (running in PM2) and web applications.  The Web website runs a web site from 
the \workspace\appfactory\dist directory.    
__NOTE:__ Depending on existing websites in IIS it may be necessary to create a virtual directory or alternate path.
This will require adjustments to the VUE_APP_REST_HOST environment variable.
  
* The rewrite plugin needs to be installed in IIS.  

  4a. Application Website  
  Create a website called Appfactory using IIS and Certificates (Development Certificates may be used for testing).
  Add two URL rewrite rules for sending HTTPS requests to the Services and Web applications running on the localhost.  
  Creation of the application website is covered in the page: [IIS Configuration](IIS-Config "IIS Configuration")    

  4b. Web Website  
  Create a website called Web using HTTP and port 8080.  Set the physical path to the 'appfactory/dist' directory.    
  Creation of the application website is covered in the page: [IIS Configuration](IIS-Config "IIS Configuration")    

5. Set System Environment Variables  
* NODE_ENV=production    
#### Postgres Connection Configuration
* POSTGRES_HOST=__*IP of Postgresql server or localhost*__
* POSTGRES_NAME=appfactory
* POSTGRES_PORT=5432
* POSTGRES_USER=appuser
* POSTGRES_PSWD=__*Postgres appuser role password*__
#### Services Callback Configuration used by Web App
* VUE_APP_PROTOCOL=https
* VUE_APP_REST_HOST=__*IP or Domain Name of this server*__/api
* VUE_APP_REST_PORT __removed or empty__  
#### Environment variables that control the sockjs callbacks from the Vue app
* VUE_APP_WEB_HOST=__*guest IP*__
* VUE_APP_WEB_PORT  __removed or empty__   
#### Environment variables are used to set development variables and the application protocol to use:
* VUE_APP_EMAIL=__*default user email*__
* VUE_APP_PSWD=__*default user password*__
* VUE_APP_MODE=DEV
* VUE_APP_LEVEL=debug

### Creating a Production Build
The Node projects can produce a production build by setting the NODE_ENV=production and running the project build:
``` javascript
set NODE_ENV=production
npm run build
```
This was done in both the services and the web project directories and populates the ./dist directory.

### PM2
> PM2 is a daemon process manager that will help you manage and keep your application online 24/7

``` javascript
npm install pm2@latest -g
```
### Starting Services REST API
The services application is run in PM2 in order to provide a Process Manager for running the Node application.
``` javascript
cd \workspace\services
pm2 start dist/index.js
```

### NOTE: with the following steps any change/update of the code requires a rebuild of the project
### NOTE: current means of running without pm2
* start cmd box with administrator rights 
``` javascript
# setup appfactory
cd \workspace\appfactory
set NODE_ENV=production
npm run build

# setup services and start them 
cd \workspace\services
set NODE_ENV=production
npm run build
set NODE_ENV=
node dist/index.js
```
* restart Appfactory and Web sites in IIS
 
