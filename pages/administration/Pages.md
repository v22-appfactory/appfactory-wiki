# Page Maintenance

##### Overview
Application pages are created using this screen.  Currently pages contain a single form and map directly to the 
application’s menu choices.  A page is created and then added to the menu tree by clicking the ‘>’ icon.  Once a menu 
item is added to the menu tree it can be positioned and edited in the menu tree.  It is necessary to Save the changes 
to the menu.

[[/images/appfactory/administration/pages.png|Page Maintenance]]

##### Fields [Required]
###### Applications
Select the application whose pages will be maintained.  Selection of the application will populate the Application Pages
datatable.
###### ID - Readonly
The record ID.
###### Title [Required]
Page title that will used at the top of the page and should be used in the navigation menu.
###### Name [Required]
Name used by the system to refer to the page.
###### Description
A text field providing more descriptive information about the page.
###### Allowed Roles
A multiselect control to select the application roles that can see the page.  Leaving this field empty allows all 
application roles to access the page.

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
The menu arrow allows a new page to be added to the navigation menu.  It is enabled when a new page has
been added but has yet to be added to the navigation menu.  Clicking the '>' button adds the page which can then
be edited in the menu tree.

##### Application Pages Datatable
Provides a list of the records in the table using the standard datatable.
###### Actions
[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Loads the record values in the fields for editing.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.
