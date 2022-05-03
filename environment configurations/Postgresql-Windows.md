Installing Postgresql on Windows consists of the following steps:
1. Install Postgresql for Windows - https://www.postgresql.org/download/windows/
2. Add postgresql bin to Path
3. Create appfactory users in psql
``` javascript
create role appowner with login password 'appowner password';  # POSTGRES-PSWD environment variable
create role appuser with login password 'appuser password';
```
4. Create database and schemas
``` javascript
-- Create database and schemas (*create-database-schemas.sql*)
CREATE DATABASE appfactory;  
-- In psql change to appfactory database
\c appfactory
-- Create schemas and change owner
CREATE SCHEMA app;  
ALTER SCHEMA app OWNER TO appowner;  
CREATE SCHEMA metadata;  
ALTER SCHEMA metadata OWNER TO appowner;
-- check schemas
\dn  
```
5. Load initial database from SQL script
``` javascript
psql appfactory < \workspace\appfactory-migrations\migrations\V1.1__initial_setup.sql
```
6. Change environment variable for POSTGRESQL to localhost
``` javascript
set POSTGRES_HOST=localhost
``` 


## Optional Steps
2a. Setup local user as Postgresql user and remove the need to enter password
  * create user _user-name_ with password null;
  * create database _user-name_;
  * alter user _user-name_ with superuser;
  * alter pg_hba.conf file login methdod from md5 to allow Trust login
  ``` javascript
  # TYPE  DATABASE        USER            ADDRESS                 METHOD

  # IPv4 local connections:
  host    all             all             127.0.0.1/32            trust
  # IPv6 local connections:
  host    all             all             ::1/128                 trust
  ```
 
 ## NOTES
 * after changing the environment variables it is necessary to re-open any cmd boxes (terminals) that are being used 
 (example: running PM2 for the services application) 
 