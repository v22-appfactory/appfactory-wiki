#### Workflow State Maintenance

##### Overview
The workflow states represent the steps in a workflow and are specific to that workflow.  Workflow states represent the
processing point that an issue is in while completing the handling of the issue.  Common workflow states would be New, 
Submitted, and Closed.  More often the state would be specific to an issue workflow.  Workflow states are specified as
state in and state out in workflow state transition. 

##### Fields
###### Name [Required]
The name for the workflow state that will be used as an option in the select control when specifying the state in and
state out in a workflow state transition.
###### Issue Type
Workflows are associated with an issue type.  The workflow is defined by workflow states and workflow state transitions.
The workflow state is associated with a workflow by specifying the issue type. 
###### Initial State
Checkbox indicating whether this state is the initial state for the workflow.
###### ID - Readonly
The record ID.
###### Description
A text field describing the workflow state.
###### Workflow Status [Optional]
The workflow status provides a short description of the workflow state.  Multiple workflow states may share the same
workflow status.  
###### Status [Optional]
The status provides additional information regarding the current status of the workflow state.  Multiple states may 
hare the same status.  

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

