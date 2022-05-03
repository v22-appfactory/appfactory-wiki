# Resource Maintenance

##### Overview
Select boxes in forms are populated by application resources which are basically references to lookup tables.  
References are created by selecting an application table and specifying the column in the table that will be used as the
text in the select control.  Currently only the Users in the system have ‘Special Processing’ which represents special 
scripting in the database to support that table.

[[/images/appfactory/administration/resources.png|Resource Maintenance]]

##### Fields
###### Applications [Required]
Select the application whose resources will be maintained.  Selection of the application will populate the Resource
Records datatable.
###### ID - Readonly
The record ID.
###### Title [Required]
Resource title that will used as an option in the resources select controls.
###### Path
Name used by the system to identify the resource.
###### Special Processing
On/off switch used to determine if special processing is used when handling resource requests.  Resources such as users
and bunos have logic specific to the resource type.
###### Table
The lookup table that contains the resource data.
###### Column
The table column that contains the label data that will be shown in the resource select control.
###### Description
A text field providing more descriptive information about the resource.

##### Buttons
###### Submit
Creates or updates the application and reloads the datatable.  When all required fields are entered the Submit 
button is enabled.
###### Clear
Cancels or clears the input allowing new records to be entered.


##### Resource Records Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.
