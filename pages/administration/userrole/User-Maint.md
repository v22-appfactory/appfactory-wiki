# User Maintenance

##### Overview
User maintenance page for maintaining user records and their group membership.

##### Fields
###### ID - Readonly
The record ID.
###### First Name
Text field for the user first name.
###### Middle Initial
Text field for the user middle initial.
###### Last Name
Text field for the user last name.
###### Email
Text field for the user email.
###### Phone
Text field for the user phone number.
###### DSN
Text field for the user DSN.
###### NPKE_EDIPI
Text field for the user NPKE EDIPI.
###### NPKE_USER
Text field for the user NPKE name.
###### NPKE_SUBJECT
Text field for the user NPKE subject.

##### Buttons
###### Submit
Creates or updates the application and reloads the datatable.  When all required fields are entered the Submit 
button is enabled.
###### Clear
Cancels or clears the input allowing new records to be entered.

##### Users Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.

##### Group Membership [Expansion Panel]
The group membership expansion panel shows a list of the groups that the user is a member of.  This is a display only
list which is updated as groups are selected in the Groups Datatable.

##### Groups [Expansion Panel]
The Groups expansion panel contains a datatable of groups and allows selection by checking the checkbox for each group.
Groups can be searched using the Search textbox at the top of the datatable.
  
Expansion panels can be shown or hidden using the arrow control in the upper right corner of the panel.
