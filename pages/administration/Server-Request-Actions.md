#Server Actions Maintenance

##### Overview
Server actions allow the configuration of actions that will be taken when making calls to the server to update data.  
Simple examples are writing to a log or history table when updating an issue or request or sending an email notification.

NOTE: The current page actions are configured using knowledge of Javascript and will need to be refined to allow 
non-programmers to configure the actions.

[[/images/appfactory/administration/server-actions.png|Server Action Page]]

##### Fields
###### Applications [Required]
Select the application whose resources will be maintained.  Selection of the application will populate the Page
Forms select control options.
###### Page Forms [Required]
Select the application page whose resources will be maintained.  Selection of the page will populate the Request
Action Records datatable.
###### ID - Readonly
The record ID.
###### Actions [Required]
The type of action to be taken is specified by selecting the action from the 'Actions' select box.  Subsequent data is
specific to the action selected.  Multiple actions are supported for any URL and as many as needed can be specified.
###### Pre/Post Processing [Required]
Actions can be specified to occur before or after the URL request processing by checking 'Pre' or 'Post'.  One or both 
checkboxes must be checked.
###### URL [Required]
Actions are associated with server requests by providing the URL for the request.  Specifiying a HTTP method or methods 
will perform the action for requests of the specified method/s.  Leaving the Methods field empty will perform the action 
for all requests to the specified URL.  Wildcards can be used when specifying the URL using Regex notation for the 
wildcard.
###### Methods
The request methods for which the action will be performed.  If left blank then the action will be performed for all
requests to the URL.
###### Action Data [Required] 
The JSON data that will be used in the server request action.
###### Format JSON
NOTE: The JSON can be formatted to making editing easier.  The JSON structure is checked when clicking the 'REFORMAT'
button or clicking SUBMIT.

[[/images/appfactory/administration/server-actions-json-format.png|Server Action Page]]

###### REFORMAT Button
Will reformat the JSON after changes.
###### Description
A text field providing more descriptive information about the server request action.
###### Template [Optional]
__TBD__

##### Buttons
###### Submit
Creates or updates the application and reloads the datatable.  When all required fields are entered the Submit 
button is enabled.
###### Clear
Cancels or clears the input allowing new records to be entered.

##### Request Action Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.

