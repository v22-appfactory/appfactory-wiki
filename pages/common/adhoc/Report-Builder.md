#### Report Builder

##### Overview
The Report Builder page allows administrators to create and run queries for any table or group of tables in the
application.  Reports can be saved and made available to other application users.  


##### Templates ==================================================
Templates for queries can be created that define the set of possible columns returned and the relationships between
the tables in the query.  Templates are reusable and can be used in multiple report queries. 

The templates select control allows the selection of the template for a report and the
 [[/images/appfactory/adhoc/template-dialog-icon.png|Template Dialog Icon]] icon launches the template dialog for
creating or editing a template.

##### Template Fields
###### Name
The unique template name.
###### Owned by user
Whether the template is owned by the current user.  Only the owner can edit an existing template.
###### Primary Table
Select control that allows the user to specify the report template's primary table.  This is the table that the query
selects from.  The select options are the tables specified in the template.
###### Entities
The Entities Panel allows the user to select tables and columns and add the to the Columns by clicking the Add Column(s)
 [[/images/appfactory/adhoc/entities-select-btn.png|Add Columns Icon]] icon.
###### Tables / Columns
The table/columns that are available to be queried.
###### Properties
The table/column properties.  The properties are shown by selecting a table or column in the 'Tables / Columns' list.
Tables and columns are deleted or removed by clicking the trash can icon in the Properties column.
   
A table shows three properties: id, relatedto, and _comment.  The id is the table ID.  The _comment is a descriptive
name to help understand the what the table contains.  The 'relatedto' property allows the linking of the table to a 
column ID in the primary table.

A selected column shows five properties: id, displayorder, label, relatedto, and _comment.
* id - the ID of the column
* displayorder - whether the column should be shown in the results by default and the order to be shown by default.  
Leave blank for columns that are available but not shown by default.
* label - the results column label
* relatedto - _TBD_ determine whether this property is used
* _comment - a description of the column data
##### Template Buttons
###### Delete
Delete the template.  Only enabled for the template owner.
###### New
Create a new template from the current template.
###### Save
Save the template.  Only enabled for the template owner or a new template.
###### Cancel
Cancels the template editing and closes the dialog.

##### Panels ==================================================
###### Entities
The Entities Panel allows the user to select tables and columns and add the to the Columns by clicking the Add Column(s)
 [[/images/appfactory/adhoc/entities-select-btn.png|Add Columns Icon]] icon.
###### Columns
The columns and order that they will be shown in the query results.  There are three possible values for each column:
the table/column name, the label, and 'Display ID'
* table/column name - the name of both the table and the column
* label - the label that will shown in the query results for the column
* Display ID - whether to return a related value for an ID or show the ID value.  Defaults to showing the related value.  
Add New Column displays a dropdown menu for the user to add a table/column to the results.  The available choices are 
based on the tables and columns that have been added to the report or template.  Hover over a table to show the table 
columns to select from.  To cancel input click off the dropdown menu.
###### Conditions
"A condition specifies a combination of one or more expressions and logical (Boolean) operators and returns a value of
TRUE, FALSE, or unknown."  The report builder conditions create SQL conditions on the server when executing the query.
Compound conditions are created by specifying 'ALL' (and) and 'ANY' (or).  Each line consists of:
* table/column - the table's column selected for the condition
* operation - the operation that will be tested in the condition, i.e. is equal to, is in list, starts with, contains, 
etc.
* value - the value to compare to using the operation
* operator - and/or for compound conditions within a group or between groups

Action icons are displayed when hovering over a group prompt or condition line.  The possible actions are:
* Add condition [[/images/appfactory/adhoc/add-condition-icon.png|Add Condition Icon]] - add a new condition to the group
* Add condition group [[/images/appfactory/adhoc/add-group-icon.png|Add Group Icon]] - add a new group 
* Delete condition or group [[/images/appfactory/adhoc/clear-icon.png|Delete Icon]] - delete the condition or group
based on which line is being hovered over 

##### Buttons Panel
###### Clear
Clears the report.
###### Load
Load an existing report.
###### Save/Del
Shows a dialog to Save or Delete the current report.
###### Results to File
Execute and save the results to a file on the server where the services API runs.  This requires an administrator to 
retrieve the results file, but is useful when executing a query with a large result set.
###### Execute
Executes the current report and displays the results in the Results datatable.

##### Results Datatable
Provides a list of the result records using the standard datatable.

