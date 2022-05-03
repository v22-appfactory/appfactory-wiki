# Role Maintenance

##### Overview
Application role maintenance page for maintaining role records and users and groups that have the applicaiton role.

##### Fields
###### Application [Required]
Select the application whose resources will be maintained.  Selection of the application will populate the Application 
Roles datatable.
###### ID - Readonly
The record ID.
###### Role Name
A text field for the name that the role will be known as.
###### Description
A text field providing more descriptive information about the role.

##### Buttons
###### Submit
Creates or updates the application and reloads the datatable.  When all required fields are entered the Submit 
button is enabled.
###### Clear
Cancels or clears the input allowing new records to be entered.

##### Application Roles Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.


##### Members [Panel]
The members panel shows a list of the role members both users and groups.  This is a display only list which is updated 
as groups and users are selected in the Groups and Users Datatable respectively.

##### Groups [Expansion Panel]
The Groups expansion panel contains a datatable of groups and allows selection by checking the checkbox for each group.
Groups can be searched using the Search textbox at the top of the datatable.

##### Users [Expansion Panel]
The Users expansion panel contains a datatable of users and allows selection by checking the checkbox for each user.
Users can be searched using the Search textbox at the top of the datatable.
  
Expansion panels can be shown or hidden using the arrow control in the upper right corner of the panel.
