## Formio Field Scripting

The formio.js forms are defined using a JSON array that consists of columns and component objects.  Very briefly the JSON
might look like the following:
``` javascript
components: [
  key: "columns",
  columns: [
    {},
    {
      components: [
        {},
        {
          key: "issuetypeid",
          type: "select",
          customConditional: "show = (data.id ? data.id <= 0 : true);"
        },
        {
          key: "issuetype",
          type: "textfield",
          customConditional: "show = (data.id ? data.id > 0 : false);"
          calculateValue: "value = (form.customData ? form.customData.formData.issuetype : '');" 
        }
      ]
    },
    {}
  ]
]
```
The formio form fields are configured using dialogs that allow them to be labeled, named, mapped to table/columns, given 
default values, and in the case of select box controls loading option values from database resources.  The control dialogs
can be customized and custom controls can be created and added to the form builder.

#### Commonly Used Component Attributes 
* key - the field name that is being used for the field
* type - the field component type
* label - the label that will be displayed 
* dataSrc - the type of source for the field data.  This is particularly significant in select controls where the options
are loaded from a database resource
* resource - the reference for the resource that will be used to fetch the resource data from the server.  This is a GUUID
in the Application Factory
* datamap - an object with attributes.  These are the data mappings onto the database table and column for the field.  The
attributes are:
  * appid - the application ID
  * categoryid - the table ID
  * fieldid - the column ID 

### Field Dialogs
Field dialogs consist of tabs such as Display, Data, Validation, API, Conditional, and Logic.  These may vary based on 
component type.  The Data and Conditional tabs allow entry of javascript to customize the field values [Custom Default
Value and Calculated Value] and visibility [Advanced Conditions].  When setting these values the user enters javascript
which can set or reference data elements in the scope of the formio component such as other field values in the form.  

### Issues with Dialog Script Entry 
Currently there is an issue when revisiting the field dialogs where the javascript previously entered is not reloaded when
returning to a dialog tab such as the Data tab.  This can lead to issues where scripting is lost when a user enters values
on the tab such as Data Source Type and does not reset the Calculated Value.  The work around is to set or reset all 
selections on the tab and saving that work prior to visiting other tabs.  Again, this is an issue that will occur on 
the Data and Conditional tabs.  This is also an issue when attempting to modify any of the scripts as they are gone and 
must be completely re-entered.  A couple of ways to check or recover the scripts are:
1. Chrome Developer Tool - view the JSON that is being downloaded when loading the form in the Network tab and examine or 
copy the script from the data.
2. Postgresql Database - copy the JSON from the __jsondata__ column in the __PAGEFORMS__ table and pasting the JSON into
a JSON viewer such as http://jsonviewer.stack.hu/ which provides formatting and Viewer or Text views of the JSON.


