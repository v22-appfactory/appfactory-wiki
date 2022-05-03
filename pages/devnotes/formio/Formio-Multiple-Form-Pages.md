# Formio Multiple Form Pages

Displaying pages that provide the ability to update multiple tables present a problem since the Applications.vue loads
a record from a single table.  An example of a page with data from multiple tables would be replicating the 
functionality in the VTAMP update issue page.

[[/images/formio forms/add-edit/vtamp-update-page.png|VTAMP Update Page with History List]]

### Querying the Second Table Data
When loading the Application.vue Vue page the form data is loaded by defining an event/action for the event _'load'_ 
performing the action _'loadedit'_ or _'loaddetail'_.  Both actions load the form.  
* Loadedit is used when navigating from a page containing a Datatable after the user selects to edit one of the lines 
in the datatable.  Prior to navigating to the maintenance page the selected row is stored in the Vuex store and when the 
loadedit action is processed the data is retrieved from the store and loaded into the form.
* Loaddetail is used in a similar way retrieveing the selected row, but then calling server using a 'url' parameter 
which calls the REST API (currently '/appform/record/:formid/:recordid' where the parameters are the form ID and the 
record ID to load).  This allows the page to customize the data that will be used retrieving related field values as 
well as the row data.    

In order to retrieve customized data for a second set of data (i.e., History records) an new action was added called 
__'relatedrecord'__ which allows calling a custom query and specifying parameters that will be sent with the request in
a POST request.
``` javascript
{"url":"/appquery/1","params":{"recordid":":id","appcolumnid":485}}
```
The JSON is used in the following way:
* url - the query to call, in this case the REST API for application queries running the query whose ID is 1.
* params - page data that is sent in a POST request as the body.  This data is retrieved from the store similar to 
'loadedit'.   
    * recordid - the record ID for the record being edited
    * appcolumnid - hard coded appcolumnid for the column that provided the foreign key relation to the record being
    edited.

The __relatedrecord__ query results are then loaded into the form's _'relatedData'_ attribute where they can be accessed
by the Formio components.

In the Work Request Maintenance screen example the secondary data is the History records for the work request.  Each
time the work request is edited a history record is created.  The history records are listed at the bottom of the page.  
[[/images/formio forms/add-edit/work-request-maintenance-with-history.png|Work Request Maintenance Page with History List]]  

### Custom Query
Custom queries are defined in the __metadata.appqueries__ table.  The rows in this table contain columns for the 
_schema_, _procname_, and _params_ for the custom query.  The _params_ sent to the procedure can be system params (
'userid' or 'serverurl') or can reference attributes in the form data.  
NOTE: The procedure in a custom query can reference a procedure that is added specifically for an application.  This 
provides a means for creating a procedure that is specific to the application's data.   

### Formio Display of the Second Table Data
#### Displaying an Array of Data
The query returning the history records returns a query.  This repeating data is handled by using a Datagrid Component 
which is basically a content component which can be populated with other components to display data and will be repeated
for each array element set in the Datagrid's 'value' attribute.  This is set in the Data tab Calculated Value using 
javascript.  
``` javascript
value = (form.relatedData ? form.relatedData : [{}]);
```
### Rendering a History Record
[[/images/formio forms/add-edit/history-record.png|History Record]]
The following is a sample of a History record's JSON:
``` javascript
  {
    "id": 1358,
    "apptableid": 121,
    "issueid": "Workflow Test",
    "startingstateid": "Mod TAR In Work",
    "endingstateid": "Mod TAR Responded by FST",
    "workflowactionid": "Respond",
    "transactiondate": "2019-10-09T13:31:52.724589+00:00",
    "details": "test complete answer",
    "authorid": "Geoff Marshall",
    "firstname": "Geoff",
    "mi": "",
    "lastname": "Marshall",
    "email": "geoff.marshal.ctr@navy.mil",
    "phone": "252-464-8744",
    "attachments": [
      {
        "path": "/apps/10",
        "uniquename": "5398f5e0-ea99-11e9-8bae-9d994806fa35_temp2.sql",
        "name": "temp2.sql",
        "size": 7969,
        "link": "http://localhost:3000/files/10/5398f5e0-ea99-11e9-8bae-9d994806fa35_temp2.sql"
      },
      {
        "path": "/apps/10",
        "uniquename": "5dddbea0-ea99-11e9-8bae-9d994806fa35_formio-scratch.txt",
        "name": "formio-scratch.txt",
        "size": 1655,
        "link": "http://localhost:3000/files/10/5dddbea0-ea99-11e9-8bae-9d994806fa35_formio-scratch.txt"
      }
    ]
  },
```
The data in the History records were rendered using HTML Components and the display of the data is described below.  The
array element being processed can be accessed using the __'row'__ object.
* Action - HTML Component; Display tab; Content javascript: 
``` javascript
<div class="well" style="font-weight: bold">Action:&nbsp;&nbsp;{{row.workflowactionid}}</div>
```
* History Transaction Date - HTML Component; Display tab; Content javascript: 
``` javascript
<div class="well">{{row.transactiondate}}&nbsp;</div>
```
* User Phone# - HTML Component; Display tab; Content javascript:
``` javascript
<div class="well">Phone:&nbsp;&nbsp;{{row.phone}}</div>
```
* Attachments - HTML Component that consists of a label and an div element where the attachment links will be created.
In the 'Custom Default Value' javascript processing is used to add a link for each element in the row.attachments (an
array).  A setTimeout is used to allow the DOM element to be rendered before attempting to append the links.    
NOTE: This was done because nesting a second Datagrid component inside of the History Datagrid component caused issues.
  * Display tab; Content javascript:
``` javascript
<div class="well">Attachments:</div>
<div id="attachments-{{row.id}}"></div> 
```  
  * Data tab; Custom Default Value javascript:
``` javascript
const div = document.getElementById(`attachments-${row.id}`);

if(div) {
  const rowId = `attachments-${row.id}`;

  setTimeout(() => {
    const divElem = document.getElementById(rowId);
	if(divElem.children.length === 0) {
      _.forEach(row.attachments, (it) => {
        const a = document.createElement("A");
		a.href = it.link;
	    a.appendChild(document.createTextNode(it.name));
        divElem.appendChild(a);
        divElem.appendChild(document.createElement("BR"));
      });
	}
  }, 200);
}
```     
* Details - HTML Component; Display tab; Content javascript:
``` javascript
<div class="well">{{row.details}}&nbsp;</div>
```
* Edit Link - HTML Component that has onClick processing that creates a __'gotoItem'__ attribute on the 
__'historyEditBtn'__ and then clicks the button.     
NOTE: This was done because nesting a Button component inside of the History Datagrid component caused issues.
  * Display tab; Content javascript:
``` javascript
<a href="javascript:void(0)"
	id={{row.id}}
	onClick="
	var element = document.getElementById('historyEditBtn');
	element.gotoItem = {key: this.id, keyAttribute: 'relatedData.id'};
  element.click();
  "
>Edit</a>
```
  * historyEditBtn - Hidden Button Component that fires 'gotoDataItem' event when clicked
    * Display tab;
      * Action - 'Event'
      * Button Event - 'gotoDataItem' 
      * Hidden

### Processing gotoDataItem event
An event/action is defined for the __'gotoDataItem'__ event with a __'navigate'__ action.  Application.vue has a 
gotoDataItem function which retrieves the item where the Edit was clicked and then processes using the 
processEditAction function that saves the item to the Vuex store and then navigates to the specified page.
  
  
