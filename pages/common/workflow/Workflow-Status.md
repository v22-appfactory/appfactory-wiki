#### Workflow Status Maintenance

##### Overview
The workflow status represents the status to be displayed for a workflow state.  Common examples would be New, 
Acknowledged, In work, Valid, Invalid, Closed, Awaiting acceptance, and Submitted.  Application specific statuses can 
also be provided.  Workflow statuses are associated with a workflow state.  

##### Fields
###### Name [Required]
The name for the status that will be used as an option in the select control when selecting the workflow status.
###### ID - Readonly
The record ID.
###### Description
A text field describing the workflow status.

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

