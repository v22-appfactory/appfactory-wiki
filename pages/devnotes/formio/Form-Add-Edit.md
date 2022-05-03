# Form Field Show/Hide/Disable Based on Add/Edit Mode

Maintenace forms need the ability to show/hide and enable/disable fields based on the mode (add/edit) that the record
is in while being edited.  The mode can be determined by whether the record being edited has an ID value.  Using this as
an indicator formiojs forms can be designed to show/hide fields and enable/disable fields on the form using the 
_'Advanced Conditions'_ scripting on the _'Conditional'_ tab of the form field settings dialog.  This will be illustrated in
the following images.

The following images show the Work Request Maintenance screen in both the add and edit modes:

##### Add a new work request.   
[[/images/formio forms/add-edit/work request maint add mode.png|Work Request Maintenance - Add Mode]]  
##### Edit an existing record changing the action to be taken on the work request and provide details.    
[[/images/formio forms/add-edit/work request maint edit mode.png|Work Request Maintenance - Edit Mode]]   

### Form Builder 

The following shows the above forms in the form builder.

##### Form Builder View of the Maintenance Screens.    
[[/images/formio forms/add-edit/form builder view of work request maint.png|Form Builder View]]   

The different field modes are achieved by having the fields on the form twice; once for the enabled component such as
a select control and once for the static display as a label.  Fields that only appear in one mode or are editable in 
both modes are on the form once and can be shown/hidden using advanced conditions.

### Field Examples

__Fields Editable in both Modes__  
The Subject and Attachment fields are active in both modes.

__Fields Enabled/Disabled in Add/Edit Modes__   
The issue type, activity, priority, and status fields are examples of fields that enabled for a new record, but are
display only in edit mode.  

##### Advanced Conditions Scripting
[[/images/formio forms/add-edit/conditional script.png|Form Builder View]] 

This snapshot shows the Issue Type field editing with the Conditional Tab and the Advanced Conditions selected.
  The scripting is done in the JavaScript field and the script shows the component when the data.id <= 0:
``` javascript
show = (data.id ? data.id <= 0 : true);
```
The label version is shown when the data.id > 0:
``` javascript
show = (data.id ? data.id > 0 : false);
```
The fields are mapped to the database differently depending on whether they are editable.  For the editable field
control the data is mapped in a normal fashion by specifying the app/table/column in the API tab:
[[/images/formio forms/add-edit/editable-mapping.png|Form Builder View]] 

For the disabled display of the field the Disabled attribute is checked on the Display tab and the Calculated Value is
scripted on the Data tab.  This loads the component value using data that is retrieved when loading the page and added 
to the formio form.   
The script from the Calculated Value in the form builder form field:
``` javascript
value = (form.customData && form.customData.formData ?
	form.customData.formData.issuetype :
	'');
```
The application script that adds the downloaded data to the formio.form so that it is available for the value update:
``` javascript
  setFormData = (data) => {
    const form = this.formio.form;
    form.customData = data;
  };
```


__Fields That Appear in only One Mode__   
The Action and Details fields only appear when editing a Work Request.  Again this is done by using the Advanced 
Conditions scripting.


  
