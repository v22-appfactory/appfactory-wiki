#### Issue Tasks

##### Overview
The Issue Tasks page allows multiple tasks to be associated with an issue.  Two datatable controls are provided, one for
selecting the issue and one for selecting tasks.  
  
The user starts by clicking the edit icon in the 'Issues' list for the issue that is being updated.  The selected issue
is shown in the 'Issue' panel.  
   
Tasks are added by selecting a task from the 'Add Tasks' list and editing the record in the 'Task' form.  When editing
is complete the task is added or updated by clicking the 'Submit' button.  Clicking the 'Clear' button clears the 
selected record and ends editing.  

As tasks are added to an issue they are shown in the 'Related Tasks' panel.  Linked tasks can be edited by clicking the 
'Edit Task' icon or removed by clicking the 'Delete Task' icon in the 'Linked Data' table. 

##### Fields
##### Issues Datatable
Provides a list of the issue records in the table using the standard datatable.  The table can be shown or hidden by 
clicking the down or up arrows respectively.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Selects the issue for editing. 

##### Issue Panel [shown when an issue is selected] 
###### Driver ID - Readonly
The selected issue driver ID.
###### RCN - Readonly
The selected issue RCN.
###### Title - Readonly
The selected issue title.

##### Related Tasks Panel [shown when an issue is selected]  
###### Linked Data Table
Lists the tasks linked with the issue.  Allows user to select a link record to be edited or deleted.

##### Task Panel [shown when a task is selected to add or a related task is selected for editing]
Shows the selected link record.  The task fields are shown for reference as readonly. 
###### Status
The status of the issue / task link.  This status is specific to the issue/task.
###### Remarks
Link record remarks.  The remarks are specific to the issue/task.
###### Submit
Creates or updates the issue/task link record.  When all required fields are entered the Submit button is enabled.
###### Clear
Cancels or clears the input and deselects the link record.

##### Tasks Datatable
Provides a list of the task records in the table using the standard datatable.  The table can be shown or hidden by 
clicking the down or up arrows respectively.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Selects the task for adding to the issue record.   
