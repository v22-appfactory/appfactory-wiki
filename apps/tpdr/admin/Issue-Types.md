#### Issue Types Maintenance
The Issue Types Maintenance screen allows a user to maintain the issue types records in the lookup table.  Each driver
type has a set of issue types which determine the workflow that will be followed for the issue.  This page allows
administrators to maintain the options that the user will see when creating an issue.  The page consists of fields for
setting the column values and a datatable that lists the application issue type records. 

##### Fields
###### Label [Required]
The label for the issue type that will be used as an option in the select control when selecting the issue type.
###### Driver Type
The driver type that this issue type is associate with.  When creating an issue once the driver type is selected the 
issue types for that driver are loaded and available for selection.
###### ID - Readonly
The record ID.
###### Description
A text field describing the issue type.

##### Buttons
###### Submit
Creates or updates the issue and reloads the datatable.  When all required fields are entered the Submit 
button is enabled.
###### Cancel
Cancels or clears the input allowing new records to be entered.

##### Issue Types Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.

