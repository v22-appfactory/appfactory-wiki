# Adhoc Report Results Overview

## Overview

_TBD_

## Topics

### Edit and Delete Rows
An adhoc report can have 'Actions' icons for edit and delete.  Result actions can be selected or the results can have
no actions.  When actions are specified it is necessary to define what action to take and the data that will be used.

#### Edit
When the user clicks on the edit icon they are navigated to a edit page in the application.  This requires an 
event/action that is specific to the report template.  The event/action is associated with the report template using
the _reporttemplateid_ column in the __formeventactions table__.

Notes:
* currently only one action is hard-coded to the Repair Task Maintenance in order to demonstrate the capabilities
* the columns to be edited must be specified in the results Columns
* prior to navigating to the edit page the application store is updated with the table row data by calling the store
function 'setEditRecord'.  The edit data is keyed by the edit page **_'pageID'_**.
* the edit page must have an event/action to retrieve the data.  This is currently supported by a load/loadedit 
event/action.
* currently the 'setEditRecord' data is created by stripping the 'tbl_' from each column name.  This only supports editing
columns from the primary query table.
