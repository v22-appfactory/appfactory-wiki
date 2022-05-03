# Developer Environment Setup

## Overview

_TBD_

## Authentication Shortcuts
Setup of environment variables can provide login and user shortcuts that will automatically login the front-end and 
automatically authenticate sessions on the server.  These environment variables are setup on the machine where the 
front and server applications are running.

#### UI
Setting the following environment variables will automatically login the user and will be the defaults in the login 
screen when selecting __Sign In__
export VUE_APP_MODE=DEV  
export VUE_APP_EMAIL=testuser@email.com  
export VUE_APP_PSWD=password  

#### Service REST API
Setting the following environment variables are set on the server will by-pass the session check and will automatically
set the session user based on the user ID provided.
export REST_APP_MODE=DEV   
export REST_APP_USERID=3575    

#### Database
_TBD_   
export POSTGRES_HOST=localhost  
export POSTGRES_USER=appuser  
export POSTGRES_PSWD=****  
export POSTGRES_NAME=appfactory  
export POSTGRES_OWNER=appowner  
export POSTGRES_OWNER_PSWD=********  

#### Flyway 
_TBD_  
export FLYWAY_HOME=/Applications/flyway-5.2.4
