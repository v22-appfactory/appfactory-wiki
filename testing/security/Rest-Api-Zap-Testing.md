# Authenticating
Prior to running tests in ZAP it is necessary to create a context and add scripting to authenticate the session prior to 
making the REST request.  

### Create Context
Click on the create context button above the Contexts/Sites Panel.  Give the context a name and save.  
[[/images/testing/security/zap-context-arrows.png|Create Context]]

### Scripting
* Display Scripts Tab
Clicking the '+' tab next to the Sites tab should allow selection of Scripts to show the Scripts Tab.  This does not 
always work so the alternative method is to selection View/Show Tab from the application menu and show the Scripts 
panel from there.  In the scripts panel and tree click on Authentication.  Right click and select 'New Script'.
* Enter a Title and save the script: "Appfactory REST Auth"
* Create request for pulling the /users/npke for the selected user
  * URL: http://localhost:3000/users/npke
  * Method: POST
  * Headers: Content-Type: application/json
  * Body:
``` javascript   
{
"email": "test.user@navy.mil",
"password": "password"
}
```
__NOTE:__ This request will return the NPKE_SUBJECT information for the user specified in the body.  This only works 
when the Environment variable VUE_APP_MODE=DEV.
__TODO:__ Capture the NPKE_SUBJECT in a global variable
* Create request to log user into session.  
  * URL: http://localhost:3000/auth/login
  * Method: POST
  * Headers:   
Content-Type: application/json  
NPKE_SUBJECT: *use value returned from /users/npke request*  
  * Body:
``` javascript   
{}
```
__NOTE:__ Making the request with a valid NPKE_SUBJECT value for a User in the database will authenticate and create a
Passport session returning cookies used in subsequent requests.
__TODO:__ Remove the hard coded NPKE_SUBJECT and set the header value from the global variable created in the 
/users/npke request.

### Add Authentication Script to Context
In the Sites Tab double click the RestApi context.  Under the Session tree expande the Contexts, expand the RestApi node
and click on the Authentication node.  
* Select the Script 'Appfactory REST Auth' and load it by clicking on the Load 
button.  
* Enter the LoginURL for where the services application is running.
* Enter a Regex pattern that indicates that the response contains the user information.
[[/images/testing/security/zap-authentication-script-dialog.png|Authentication Script Dialog]]
* Save by clicking OK

### Import OpenApi File for the Endpoints to Test
* Select Import/Import an OpenAPI definition from the local file system
  * File Path: *path/to/openapi/file*
  * Target URL: *url for the services application: example: http://localhost:3000*
  * Click Import button  
  
If the import is successful the endpoints will be added to the Sites tree.
[[/images/testing/security/zap-imported-site-endpoints.png|Imported site endpoints]]

### Running Fuzzing Attacks Against an Endpoint
* Select an endpoint in the Sites tree, right click and select Attack/Fuzz;  This will display a dialog box.  
[[/images/testing/security/zap-fuzz-dialog.png|Fuzz attack dialog]]    
The next step is probably the most complicated step with a number of variations depending on the request method 
(GET, POST, PUT, DELETE) and what in the OpenAPI description needs to be replaced.  There are three possibilities for 
what aspects of the request can be substituted for with various attack substitutions:
1. Header value
2. URL path
3. Request body
Fuzz Locations (right side) are specified by selecting a Header or Body value (left side) and clicking the Add button.
#### Fuzzing Authentication
It is important to note that in order for the Context Authentication to be run while running the Spider or Fuzzing tests
it is necessary to enable Forced User Mode.  This is done by simply clicking the 'Forced User Mode' button to enabled,
but it is very easy to miss since the default is set to disabled.
[[/images/testing/security/zap-forced-user-mode.png|Forced User Mode]]    

#### URL Path Value
In the image above the value in the URL to change would be 'appId':  
 PUT http://localhost:3000/applications/appId HTTP/1.1   
 This needs to be substituted with a valid application ID as the actual endpoint route is /applications/:appId.  In this
 example the test data has an application with an ID of 10.  So the 'appId' is highlight and the Add button is clicked.
    
[[/images/testing/security/zap-replace-url-path.png|Steps to replace URL path element]]

#### Body Value
In a similar way a value in the body JSON can be changed by clicking in the Body panel, selecting text (NOTE: it is best
to select the text inside of the quotes), and clicking the Add button.  The following steps will replace the selected 
text with multiple Fuzz attack values:
* In the 'Payloads' dialog click Add
* In the 'Add Payload' dialog select:
  * Type: File Fuzzers
  * expand jbrofuzz
  * check 'Buffer Overflows'
  * check 'SQL Injection'
  * click Add button : 'Add Payload' dialog
* Click OK button : 'Payloads' dialog
* Click Start Fuzzer button in the 'Fuzzer' dialog

These steps will replace the selected strings with the values specified in the 'Add Payload' dialog/s.  The results can
be inspected in the Fuzzer tab at the bottom of the screen.  The Services application console can also be inspected for
what takes place on the Services server.
  
    
    
 

