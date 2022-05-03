Remote Queries consist of a adhoc query request made either from the Application Factory user interface (UI) or by 
making an HTTP request (POST) using another application or a utility such as curl or Postman.  The request is a POST 
request to the Application Factory REST API server with JSON query parameters in the request body.  Authentication 
requires a user session instance and the session cookie sent in the request header.  Query results are returned as a 
JSON result set that contains headers and result rows.  The results can be returned as HTTP results or stored on the 
application server and transferred by some other means.

## URL
Calls are made to:  
http://__*serverurl*__:__*port*__/adhoc/__*:appId*__  
https://__*serverurl*__/api/adhoc/__*:appId*__   

## JSON Request Body
The request JSON consists of an array of columns that will be returned and a 'whereClause' object that has an operator
and nested arrays of query conditions.  It is important to note that the query JSON does not have to be written by hand
as JSON but can be generated from the three Adhoc query screens (Report Builder, Ad Hoc Report, or Simple Query). The 
query JSON is used on the server to construct a SQL request on the server which is then executed against the application
database.

Sample request JSON sent in the request body.  
[[/images/remote query/json-request-viewer.png|Example query request JSON]]

### Columns
The columns list determines what data is included in the SQL Select clause and returned from the query.  The columns are
a simple array of column objects that have the following properties:
* id - the __appcolumns__ table ID
* label - the label to display 
* value - used for foreign key IDs to flag whether to return the actual column ID value (true) rather than the
referenced data (false) 
* linkColumn - how the referenced column is handled in the database; This handles the differences between column names
and JSON column names. (example of column inside a JSON column: `jsondata->>'issueid'`)
* linkColumnId - the __appcolumns__ table ID for the column in the referencing table.  
[[/images/remote query/request-column-linkcolumn.png|Example of use of linkColumn and linkColumnId]]   
In this example linkColumnId: 485 is the History.issueid which references a WorkRequest record.  The column to be shown
is id: 464 which is the WorkRequest.issuetypeid which references a IssueTypes record and will display the 
IssueTypes.label value from that record.  In this way queries can handle two levels of reference, i.e. History => 
WorkRequest => IssueTypes showing the name of the issue type. 
  
### Where Clause
The where clause is an object that contains nested conditions.  The objects have the following properties:
* operator - 'any' or 'all' which translate into the query operators 'OR' and 'AND' respectively.
* conditions - the query conditions which can either have a type of 'condition' or 'group'
* type - types are:
  * 'group' - a group of nested conditions
  * 'condition' - an actual condition that is translated into SQL in the WHERE clause
* data - the condition data 
  * id - query operation (examples: "StartsWith", "Contains", "Equal", "InList", "NotStartsWith", "NotContains", 
  "NotEqual", "NotInList")
  * data - template used to create the SQL condition. (example: "|501| `[[starts with]]` {Reply}")
    * |501| - __appcolumns__ table ID
    * `[[starts with]]` - condition operator that is replaced with the appropriate Postgres operator
    * {Reply} - the condition value
  * ref - the __appcolumns__ table ID for the column that references another table
  * key - reference information for the __apptables__ ID and appcolumns ID.  The key captures the __apptables__ ID for
  the referencing column.
  In this example the ref: 488 is the History.workflowactionid that references a WorkflowAction record and id: 501 is 
  the column (WorkflowAction.name) in that record that will be used in the condition.

 ## Results   
The results are returned as JSON containing an array of 'headers' and an array of 'results'.

Sample response JSON.   
[[/images/remote query/json-response-viewer.png|Example query response JSON]]

### Headers
The header array consists of header objects with the following properties:
* text - the header text or label
* value - the column key that will be used in the results object
* columnname - the __appcolumns__ table ID
* displayorder - the column order in the results datatable
* datatype - the column data type (integer, string, timestampe, etc)
* tablename - the __apptables__ table ID
### Results
The results array consists of results rows with column key/value pairs.
* key - the column key which matches one of the header 'values'; examples: 'tbl_id', 'issues_issueid', 
'issuetypes_issuetypeid' 
* value - the column value for that row; examples: 928, "Test Closed", "Modification"
### Results to File
For large results sets it is possible to save the results to a file on the REST API server.  This can be done in the 
Report Builder UI by selecting 'Results To File' when executing the query.

Results To File button in the UI. 
[[/images/remote query/results-to-file-btn.png|Results To File button]]
Results To File Message in the Report Builder UI.
[[/images/remote query/results-to-file-message.png|Results To File message]]

This adds a third property to the JSON request body with a report title:  
``` javascript
outputToFile: "Simple Query 4 Groups"
```
The HTTP request response will contain the name of the json file including the user email for the requestor and a .json
extension:
``` javascript
Simple-Query-4-Groups__geoff.marshal.ctr@navy.mil.json
```

## Authentication
If a adhoc query request is made without a valid session then the response will be 'Invalid session.'.  Requests made
from the UI Report Builder page will require a session in order to access the Report Builder page and the results are
either displayed in the 'Results' datatable at the bottom of the screen or saved to a file as described above.
Requests made from a tool such as postman will need to send a request to start a session and will then need to include 
the session cookie with the query requst.  Postman will include the cookie automatically after a successful login 
request.

### Postman Request Steps
The request to login are made as a POST to /auth/login with specific Headers.  The NPKE_SUBJECT must contain a valid
value that is in the application factory __users__ table.  A session is created for the matching user and any data 
access will be based on the session user's roles.
  
Calls are made to:   
http://__*serverurl*__:__*port*__/auth/login  
https://__*serverurl*__/api/auth/login  

Headers:               
* Content-Type: application/json
* NPKE_SUBJECT: __*a valid npke_subject as created by the BIG IP proxy*__
* NPKE_TYPE: CAC

Response cookies:
* mysession
* mysession.sig

The response cookies should then be added to the query request headers as:
* Cookie:  mysession=eyJwYXNzcG9ydCI6eyJ1c2VyIjozNTc1fX0=; mysession.sig=h-t5gK2g4CYR05jW55BuxKhKIGI



