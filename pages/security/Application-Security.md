# Application Pages

## Overview

_TBD_

## Sessions
User sessions are maintained using Passport (https://www.npmjs.com/package/passport) on the server and returning tokens 
containing serialized user IDs to the front-end which are returned on subsequent requests.  Passport is middleware
which works with Express allowing each request to be checked for a valid session prior to executing the request.  By
retrieving the user information it is possible to pass the current user to the request in order to check for 
authorization for the request.

#### Server
##### Adding a middleware call
A call for checking the session status and finding the user can be added to an Express routing by adding a second 
parameter to the routing.  In the following example the call to _authController.authCheckUser_ has been added which
will check that a session exists based on a token sent as a part of the request and passing the current user information
to the pageformFindById request.
``` javascript
pageRoutes.get('/forms/:appId/:pageId', authController.authCheckUser, controller.pageformFindById);
```
##### Updating middleware calls and passing data to the following requests
The following is an example of a middleware session check which retrieves the current user information and adds it to 
the results parameter using _res.locals_ which can be used in processing later in the middleware chain. 
``` javascript
exports.authCheckUser = async (req, res, next) => {
  let user = null;
  if (req.isAuthenticated()) {
    user = await findUser(req.session.passport.user);
  }
  res.locals.user = user;
  return next();
};
```

##### NOTE regarding requests to the server: _withCredentials_   
It is important to remember that when making axios calls from the browser it is necessary to explicitly indicate that 
the request should include credentials as a part of the header.  This is done by adding the _withCredentials_ flag.   
Example:
``` javascript
      axios.get(
        `${context.getters.serverUrl}/pages/forms/${payload.appid}/${payload.pageid}`,
        { withCredentials: true, headers: context.getters.serviceHeaders }
      )
```
   