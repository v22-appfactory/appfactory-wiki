#### Driver Types Maintenance

##### Overview
The driver types maintenance form allows the entry and editing of the driver types lookup table used in an issue.
Driver types supported include TPDR, EIR, TD/TCTO, etc.  Each driver type can have multiple issue types which determine
the workflow used for the issue.  

##### Fields
###### Name [Required]
The name for the driver type that will be used as an option in the select control when selecting the driver type of an 
issue.
###### ID - Readonly
The record ID.
###### Description
A text field describing the driver type.

##### Buttons
###### Submit
Creates or updates the priority and reloads the datatable.  When all required fields are entered the Submit 
button is enabled.
###### Cancel
Cancels or clears the input allowing new records to be entered.

##### Driver Types Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.

