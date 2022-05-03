# Deployment Notes

## Postgres / Appfactory Initialization
* open CMD box (terminal) Run as administrator
* CD into migrations folder and pull master branch
``` javascript
cd \workspace\appfactory-migrations
git pull origin master
```
* open 2nd CMD box (terminal) Run as administrator and start psql
* drop and create appfactory database
* create schemas and set owner to appowner
* check schemas
* quit psql
``` javascript
psql
gmarshall=# drop database appfactory;
DROP DATABASE
gmarshall=# create database appfactory;
CREATE DATABASE
gmarshall=# \c appfactory
You are now connected to database "appfactory" as user "gmarshall".
appfactory=# create schema app;
CREATE SCHEMA
appfactory=# alter schema app owner to appowner;
ALTER SCHEMA
appfactory=# create schema metadata;
CREATE SCHEMA
appfactory=# alter schema metadata owner to appowner;
ALTER SCHEMA
appfactory=# \dn
   List of schemas
   Name   |  Owner
----------+----------
 app      | appowner
 metadata | appowner
 public   | postgres
(3 rows)
appfactory=# \q
```
* return to 1st CMD box
* load data from migrations\V1.1__initial_setup.sql
``` javascript
psql appfactory < migrations\V1.1__initial_setup.sql
```
## Services Application
* open CMD box (terminal) Run as administrator
* CD into servcies folder and pull master branch
* pull services repo
* set NODE_ENV to production
* build services application updating ./dist folder structure
* start services application
``` javascript
cd \workspace\services
git pull origin master
set NODE_ENV=production
npm run build
node dist\index.js
```

## Vue Application
* open CMD box (terminal) Run as administrator
* CD into servcies folder and pull master branch
* pull services repo
* update node_modules folder tree; it may be necessary to delete node_modules & reinstall if build step hangs
``` javascript
cd \workspace\appfactory
git pull origin master
npm install
```
* stop Web site in Internet Information SErvices (IIS) Manager
* set NODE_ENV to development
* build appfactory application updating ./dist folder structure
* restart Web site in Internet Information SErvices (IIS) Manager
``` javascript
set NODE_ENV=development
npm run build
```

## Deploying to a Server with no Internet Access
Normally the Node and Vue projects are deployed using __'git clone'__ to download the code and then __'node install'__
to build the dependencies in the __'node_modules'__ directory.  Then the *compiled* code is built in the __'./dist'__
directory producing code that is ES5 compliant and will run in any browser.  

These steps require Internet access to retrieve dependencies which may not be available.  In order to work around this
restriction it is possible to build the project externally and take a snapshot of the directories.  This can be done 
using the following:
* Tar - using the *node pack* to generate a tarball and the *tar* command to expand on the destination server.  The
advantage is a smaller package that can be adjusted to have just the needed components.
* ZIP - using zip to capture the whole directory including development components.  The advantage is that ZIP is 
guaranteed to be present on a Windows server.

#### Common Steps to Prepare the Directory
The following steps are done on a workstation with Internet access:
``` bash
git pull origin master
npm install
set NODE_ENV=|production/development|
npm run build
```

#### ZIP
Capture the application directory using the windows command to 'send to compressed folder':
* right click on the directory 
* select *Send to*
* select *Compressed (zipped) folder*
This will create a *.zip file that can be uploaded to the server.  Once on the server the file is unzipped by right 
clicking on the file and choosing *Extract all*.   
Once the folder is unzipped and named correctly it can be used as normal depending on the services or appfactory
directory.

#### TAR
A compressed tarball can be created by running the command *npm pack*.  The contents can be controlled by specifying 
what to ignore (.npmignore) and what dependencies to retrieve from the node_modules (bundledDependencies in the 
package.json file).  The .npmignore and package.json files are contained in the project repositories.  
The following cmdline will produce a .tgz tarball:
``` bash
npm pack
```
The tarball can be updated to the the target server and unpacked using:
``` bash
tar -xvf |name of the .tgz|
```
Once the folder is unzipped and named correctly it can be used as normal depending on the services or appfactory
directory.

__*NOTE:*__ Using both techniques has been discussed using the following steps to produce a minimized ZIP that can be
easily unzipped on a Windows server:
1. *npm pack* to produce a minimal production directory
2. unpack the .tgz file into a directory
3. zip the production directory producing a .ZIP file for upload
 







