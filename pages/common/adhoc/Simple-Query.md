#### Simple Query

##### Overview
The Simple Query page provides the simplest user interface allowing users to customize and run queries in the 
application.  Reports are created in the Report Builder and shared for others to customize columns and conditions.  

##### Panels ==================================================
###### Columns
The columns and order that they will be shown in the query results.  Each column has two subcolumns:
* table/column name - the name of both the table and the column
* label - the label that will shown in the query results for the column

Add New Column displays a dropdown menu for the user to add a table/column to the results.  The available choices are 
based on the tables and columns that have been added to the report or template.  Hover over a table to show the table 
columns to select from.  To cancel input click off the dropdown menu.

Columns can be reordered using drag-n-drop and removed by hovering over the line and clicking the clear icon
 [[/images/appfactory/adhoc/clear-icon.png|Delete Icon]] .
###### Conditions
"A condition specifies a combination of one or more expressions and logical (Boolean) operators and returns a value of
TRUE, FALSE, or unknown."  The report builder conditions create SQL conditions on the server when executing the query.
Compound conditions are created by specifying 'ALL' (and) and 'ANY' (or).  Each line consists of:
* Select Field - the table's column selected for the condition
* Select Operation - the operation that will be tested in the condition, i.e. is equal to, is in list, starts with, 
contains, etc.
* Search Value - the value to compare to using the operation
* Logic - and/or for compound conditions within a group or between groups

Action icons are displayed when hovering over a group prompt or condition line.  The possible actions are:
* Add condition group [[/images/appfactory/adhoc/add-group-icon.png|Add Group Icon]] - add a new group 
* Add condition [[/images/appfactory/adhoc/add-condition-icon.png|Add Condition Icon]] - add a new condition to the group
* Delete condition [[/images/appfactory/adhoc/clear-icon.png|Delete Icon]] - delete the condition based on which line is
being hovered over 
* Delete group [[/images/appfactory/adhoc/delete-group-icon.png|Delete Icon]] - delete the group

##### Buttons Panel
###### Clear Query
Clears the report.
###### Load Query
Load an existing report.
###### Save/Del Query
Shows a dialog to Save or Delete the current report.
###### Execute
Executes the current report and displays the results in the Results datatable.

##### Results Datatable
Provides a list of the result records using the standard datatable.

