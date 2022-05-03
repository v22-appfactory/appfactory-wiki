#### Workflow Actions Maintenance

##### Overview
The workflow action represents the actual action being taken when transitioning from one state to another.  Common 
examples would be Acknowledge, Reject, Accept, Invalidate, Validate, Close, Submit, and Update.  Application specific 
actions can also be provided.  Workflow actions are associated with a workflow state transition.  

##### Fields
###### Name [Required]
The name for the action that will be used as an option in the select control when selecting the workflow action.
###### ID - Readonly
The record ID.
###### Description
A text field describing the workflow action.

##### Buttons
###### Submit
Creates or updates the priority and reloads the datatable.  When all required fields are entered the Submit 
button is enabled.
###### Clear
Cancels or clears the input allowing new records to be entered.

##### Issue Types Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.

