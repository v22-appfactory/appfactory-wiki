# Form Actions Maintenance

##### Overview
Form actions allow the configuration of actions that will be taken when events occur while interacting with a form.  
Simple examples are navigating to different page after successful submission of a record or loading data when opening a 
page.

NOTE: The current page actions are configured using knowledge of Javascript and will need to be refined to allow 
non-programmers to configure the actions.

[[/images/appfactory/administration/form-actions.png|Form Action Page]]

##### Fields
###### Applications [Required]
Select the application whose resources will be maintained.  Selection of the application will populate the Page
Forms select control options.
###### Page Forms [Required]
Select the application page whose resources will be maintained.  Selection of the page will populate the Request
Action Records datatable.
###### ID - Readonly
The record ID.
###### Events [Required]
The event that will trigger the action. Events are of the type: add, delete, edit, goto, load, etc.
###### Actions [Required]
The type of action to be taken is specified by selecting the action from the 'Actions' select box.  Subsequent data is
specific to the action selected.
###### Action Data [Required]
The JSON data that will be used in the action specific to the action being performed.  
Example: {"url":"/appquery/1","params":{"recordid":":id","appcolumnid":485}}

##### Buttons
###### Submit
Creates or updates the application and reloads the datatable.  When all required fields are entered the Submit 
button is enabled.
###### Clear
Cancels or clears the input allowing new records to be entered.

##### Action Records Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.

