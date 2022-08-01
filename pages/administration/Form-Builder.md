# Form Builder

##### Overview
Application forms are built in the ‘Form Builder’ page using the form.io form builder interface.  The user can select 
the application page and specify a table whose data the form represents.  Forms are built by dragging layout or control 
components from the left side of the page onto the form.  Each field can then have a resource and/or table column 
associated with it.  The resources are loaded onto a loaded form at runtime and after submission the table column will 
be updated with the data from the form.

NOTE: Currently only one form can be added to a page.

[[../../images/appfactory/administration/form-builder.png|Form Builder Page]]

##### Fields
###### Applications [Required]
Select the application whose page forms will be maintained.  Selection of the application will populate the Pages
select control options.
###### Pages [Required]
Select the application page whose form will be maintained.  Selection of the page will populate the form if a form is
associated with the page.
###### Forms
A list of pagess used in the same way as the Pages select control.  This allows the users to see all pages while 
selecting. 
###### ID - Readonly
The record ID.
###### Tables
Select the table that the form maintains.
###### Columns
Select the column used to update the form record.  This is generally the record ID.
###### Description
A text field providing more descriptive information about the page form.

##### Buttons
###### Submit
Creates or updates the page form.  When all required fields are entered the Submit button is enabled.  Remember to save
form changes by clicking the Submit button.
###### Clear
Cancels or clears the input allowing new records to be entered.

##### Formio Form Builder
The form is created by using the canvas at the bottom of the page.  Detailed information on the form builder can be
found at: https://www.netiq.com/documentation/identity-manager-48/FormioHelp/userguide/form-components/

###### Components
Components are selected from the expansion panels on the left side of the area.  The component groups are:
* Basic
* Advanced
* Layout
* Data
* Premium    
Clicking on a component panel shows its component types which can then be dragged onto the form canvas.

###### Form Canvas
The form canvas is located on the right side and has a blue area with the label 'Drag and Drop a form component'.

Forms are created by dragging components from the left side of the form builder and placing them in the form on the
right side of the form builder.  Layout can be done by selecting a Layout component, placing it on the form and then
adding other components in the layout component.  A simple example would be to drag a Columns layout component onto the
form, configure the number of columns, and then dragging Basic, Advanced, or Data components into the columns.

Components are edited by hovering over the component and then clicking on one of the action buttons shown while 
hovering.  The edit button is the 'gear' button and shows a dialog with tabs which allow the component to be configured.
Details of the component configuration are covered in the Formio Form Builder link.  Configuration information specific
to the Appfactory are discussed below.

###### Data Tab
Select controls can have a resource associated that provides the options from an application resource table.
* Data Source Type - select 'Resource' and the application resources will be loaded into the Resource select control.
* Resource - the list of application resources are available for selection.  The resource selected will be loaded when
the form is loaded in the application.

Custom data can be configuread int the 'Calculated Value' field.  This allows the field component to be loaded using 
javascript to set the component value using data loaded in the form object.

###### API Tab
Form components are mapped onto the form table columns using the API tab.  Fields are mapped by selection the 
Application, Categorym, and Test Field Mapping.  
* Application - select the application
* Category - select the application table
* Test Field Mapping - select the column

As each selection is made the next control's options are loaded for the selection.
