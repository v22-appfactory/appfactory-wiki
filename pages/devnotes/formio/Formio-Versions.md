## Formio Versions

The following are notes regarding some of the issues encountered when upgrading the formiojs library.

### 3.0.0 => 3.22.15

#### 1. Select Component attributes were added
Approximately 13 attributes were added to the Select component.  Due to the changes existing select component fields 
did not load correctly causing the Resources to not load and breaking the mapping to the database table/column.  The 
solution was to edit each component (all types) and reselect the Resources and API setting for the table/column.  No
determination was made for what caused the load failure. 
#### 2. The choice select library changed the name of the function to select an option from existing data
Choices is a select control library used by the formio select component.  The function to set the select option changed
from __setValueByChoice__ to __setChoiceByValue__ which caused an error.  Changing to the new name resolved the issue and the
function continued to work as before. 
#### 3. The select component option data changed for new Select component fields.
This one is particulary strange since existing form select components continued to have option data in the old format
while any new select component fields added to a form contained option data in a new format.
* Old Format
``` javascript
{ 
  value: { 
    label: 'label string', 
    value: integer/string/object
  } 
}
```
* New Format
``` javascript
{ 
  label: '<span>label string</span>', 
  value: integer/string/object
}
```
The solution was to create a __getNormalizedObject__ function which will return either format into a common object.

