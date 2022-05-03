# Application Maintenance

##### Overview
Applications are created and maintained in this screen.

[[/images/appfactory/administration/application.png|Application Maintenance Page]]

Once an application has been created it can be added to the menu using the Menu dropdown list.  Clicking the ‘>’ icon 
will add the menu tree where it can be moved to the appropriate position.  It is necessary to click the menu Save button 
to save the menu change.
 
[[/images/appfactory/administration/application-menu.png|Application Maintenance Menu]]
 

##### Fields
###### ID - Readonly
The record ID.
###### Name [Required]
The name for the application and how it will shown in the navigation menu.
###### Short Name [Required]
Additional descriptive name.  Currently not used.
###### Description
A text field providing more descriptive information on the application.

##### Buttons
###### Submit
Creates or updates the application and reloads the datatable.  When all required fields are entered the Submit 
button is enabled.
###### Clear
Cancels or clears the input allowing new records to be entered.

##### Menu
###### Button Bar
* SAVE - persist all changes
* Expand All - expands all directory nodes
* Close All - closes all open directory nodes

###### Menu Tree
The menu tree provides editing of the navigation menu that appears on the left side of the page.  The menu item actions
are accessed by hovering over the item to modify and are shown to the right of the label.  The menu tree supports:
* Add node - a menu node is similar to a folder and can contain menu leaf nodes.  An application is added as a node 
* Add leaf - a leaf represents a application page 
* Edit item - Changes can be made to the name shown in the menu tree
* Deleting an item - directory nodes and leaf nodes can be deleted
* Drag and drop positioning    

Changes to the menu tree are made persistent by clicking the 'Save' button at the top of the menu tree. 
 
###### Menu Arrow
The menu arrow allows a new application to be added to the navigation menu.  It is enabled when a new application has
been added but has yet to be added to the navigation menu.  Clicking the '>' button adds the application which can then
be edited in the menu tree.

##### Application Records Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.
