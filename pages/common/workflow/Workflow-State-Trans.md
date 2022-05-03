#### Workflow State Transitions Maintenance

##### Overview
The workflow states transitions represent changes in workflow state from one workflow state to another.  State 
transitions provide the means of moving an issue through a workflow and are specific to workflow states.  Workflow 
states can have multiple state transitions which represent the actions that can be taken when an issue is in a 
particular state and identify the resulting state.  

##### Fields
###### Label [Required]
The label for the workflow state transition that will be used as an option in the select control when selecting the 
workflow state transition that is taking place.
###### Roles [Multiselect]
Selecting workflow state transitions can be restricted to users in specific roles.  If roles are specified then only 
users in those roles can specify that a transition has occured.  This allows specific user roles to move an issue 
through the workflow depending on the workflow state.  If no roles are specified then the state transition can performed
by any application user. 
###### ID - Readonly
The record ID.
###### State In
State transitions take place between states.  This field specifies the state being transitioned from.  
###### State Out
State transitions take place between states.  This field specifies the state being transitioned to.  
###### Action
The workflow action provides a short description of the actual action that is taking place during the workflow state
transition.   

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

