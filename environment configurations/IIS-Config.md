IIS (Windows Internet Information Services) configuration builds on the 
[Windows Configuration](Windows-Config "Windows Configuration") replacing the commandline and IDE running of the 
services and web applications and instead running in them in IIS and PM2.  IIS also provides a reverse-proxy and allows
the applications to be run from the browser using SSL/HTTPS.

## Environmental Variables running in IIS
The following changes to the environment variables are needed for running in IIS using HTTPS:  
VUE_APP_PROTOCOL=https   
VUE_APP_REST_HOST=__*guest IP*__/api   
VUE_APP_REST_PORT __removed or empty__  
VUE_APP_WEB_PORT  __removed or empty__   

## Creating a Production Build
The Node projects can produce a production build by setting the NODE_ENV=production and running the project build:
``` javascript
set NODE_ENV=production
npm run build
```
This was done in both the services and the web project directories and populates the ./dist directory.

## PM2
> PM2 is a daemon process manager that will help you manage and keep your application online 24/7

``` javascript
npm install pm2@latest -g
```
# Services REST API
The services application is run in PM2 in order to provide a Process Manager for running the Node application.
``` javascript
cd \workspace\services
pm2 start dist/index.js
```

# IIS Configuration
### Rewrite Plugin
The rewrite plugin was downloaded from https://www.iis.net/downloads/microsoft/url-rewrite and installed.  

Two IIS websites were created: Appfactory and Web.  The Appfactory application is used as a reverse-proxy which will 
redirect HTTPS requests to the services (running in PM2) and web applications.  The Web website runs a web site from 
the \workspace\appfactory\dist directory.

#### Application Website
Create a website called Appfactory using IIS and Development Certificates.  Add two URL rewrite rules for sending HTTPS
requests to the Services and Web applications running on the localhost.
__Application Website Bindings__   
[[/images/IIS and windows/appfactory website bindings.png|Application Website Bindings]]    
[[/images/IIS and windows/appfactory website advanced settings.png|Application Website Advanced Settings]]   
__Application Website URL Rewrite Rules__  
[[/images/IIS and windows/appfactory website rewrite rules.png|Application Website URL Rewrite Rules]]  
__NOTE:__ The rewrite rule for the services using api/ in the URL will rewrite the call to http://localhost:3000 
removing the api from the URL.  The rewrite rule for the web application sends the request to http://localhost:8080.  It
is important that the services rule precedes the web rule.

#### Web Website
Create a website called Web using HTTP and port 8080.  Set the physical path to the 'appfactory/dist' directory.    
__Web Website Bindings__   
[[/images/IIS and windows/web website bindings.png|Web Website Bindings]]    
[[/images/IIS and windows/web website advanced settings.png|Web Website Advanced Settings]]   


## NOTES
* Any changes to the source require a rebuild of the ./dist directory.
* Changes to the web application require that the Web website be restarted to guarantee that the page will not be cached.
  

