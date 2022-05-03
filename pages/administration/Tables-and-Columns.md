# Table and Column Maintenance

##### Overview
Application tables and table columns are defined and maintained on this page.  All data tables have an application ID 
column which specifies that the data belongs to the specified application.  Once tables and their columns are defined 
they can be used as application resources and/or as the data source for an application form.

Tables are one of four types:

1. Lookup - an existing system lookup table (Activity, Status, Priority, Issue Type, etc.)
2. Issue - an existing issue  table that has a combination of predefined columns and columns added for the application.
3. Custom Lookup - a custom lookup table with ID, Label, and Description columns.
4. Custom Table - a custom table with completely custom columns.

[[/images/appfactory/administration/tables-add.png|Add table type]]

 Application tables and columns are displayed in the ‘Tables’ dropdown on the right side of the page.  Both tables and 
 columns are edited by selecting them in the dropdown, editing them in the forms, and submitting the changes.

[[/images/appfactory/administration/tables.png|Table list and detail]]

Columns can be references to lookup tables or data stored as JSON in a json column.  When a table is created some 
columns are generated automatically for the specific table type.  Additional columns can be added to customize the table
 for the application.

[[/images/appfactory/administration/column-add.png|Add column]]

#### Page Areas
##### Applications [Required]
Select the application whose tables/columns will be maintained.  Selection of the application will populate the Tables
list.
##### Tables [Expansion Panel]
The tables expansion panel shows a list of the application tables.  Tables can be edited using the actions icons.  The
panel can be shown or hidden using the arrow control in the upper right corner of the panel.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.

##### Table Information [Form]
A table can be created or edited using the Table Information form.  Clicking the SUBMIT button will persist the
information and clicking the CLEAR button will clear the form.  See below for form details.
##### Columns [Expansion Panel]
The columns expansion panel shows a list of the columns in the table.  Columns can be edited using the actions icons.  
The panel can be shown or hidden using the arrow control in the upper right corner of the panel.
##### Column Information [Form]
A column can be created or edited using the Column Information form.  Columns are edited by selecting the table and
then selecting the column or adding a new column.  Clicking the SUBMIT button will persist the
information and clicking the CLEAR button will clear the form.  See below for form details.


##### Table Information Details
###### ADD [New records only; hidden in Edit mode]
Creating a new table is started by clicking the ADD button and selecting the table type form the floating menu.
###### ID - Readonly
The record ID.
###### Mode [Readonly in Edit mode]
Displays the table type.
###### Label
The label for the table that will be used in table selection controls.
###### System Table
The underlying system table that will hold the table records.  If the table used is defined by the system then the field
is readonly (Custom Table, Custom Table, and Issue Table).  When adding a Lookup Table the underlying system table is
selected by the user based on the type of data (columns) desired.  
###### Table Name [Readonly]
Displays the actual table name for the system table.
###### Description
A text field providing more descriptive information about the table.

##### Column Information Details
###### ID - Readonly
The record ID.
###### Label [Required]
The label for the column that will be used in table selection controls.
###### Column Name [Required] (select control and textbox)
Columns are either pre-defined columns for the system table selected above or a JSON column for a custom column.  If a
pre-defined column is selected in the select control then a readonly display of the column name is shown in the textbox.
If the JSON Column is set to true then the select control is disabled and a name must be typed in the textbox.  The name
in the textbox will be used as the attribute in the JSON column.  This is the actual column name used in the database.
###### JSON Column
Use a pre-defined table column (false or off) or create a custom JSON column (true or on).
###### Data Type
For a custom column the data type determines the data that will stored in the column.
###### Length
The maximum length of the column for text or varchar columns.
###### Name
_TBD_ - not used and should be removed
###### Display Order
The order that the column will be shown in a datatable.  Leave blank if the column is not shown in a table datatable.

###### Lookup Table Reference
__NOTE:__ This section needs review for how the various columns/values are used.
* Lookup Table - The selection of the application table that is referenced by this column.
* Master Table [Readonly] - The actual system table name of the lookup table.
* Master Column - The lookup table column that is referenced by this foreign key.  This is generally the ID of the 
lookup table.
* Master Display - The lookup table column that is displayed.  This is the column whose value will be shown in place of 
the foreign key id.  The master display can be the concatenation of multiple fields.  [Example: users.firstname || ' ' 
|| users.lastname]
* Reference Table - The selection of the application table that is referenced by this column.
* Reference Columns - The lookup table column that is displayed.  This is the column whose value will be shown in place of the foreign key id.
* Reference Column [Readonly] - The actual column ID of the reference column.


