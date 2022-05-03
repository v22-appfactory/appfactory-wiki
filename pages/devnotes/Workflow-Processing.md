# Workflow Processing

## Current Workflow Processing
Currently all workflow processing occurs when submitting data from a form and doing an add or update to the form table.
The form data must contain a field indicating what Workflow State is involved; an add requires an 'issuetypeid' and an 
update requires a 'statetransitionid'.  The state processing steps are the following:
* Check for required state field: add/issuetypeid or update/statetransitionid. [__appformController.js__]
* Check the form table for whether it is an 'Issue' table and has a flag set to indicate that the table has workflow state.
[procedure: __appformGetFromTables__]
* Get the workflow state data by calling procedure workflowStateTransition and adds state data (__workflowstateid__ and 
__workflowactionid__) to the request data.
* Call form add/update procedure: __formRecordAdd__ or __formRecordUpdate__.
* The procedures return the results of a query on the table row (__formRecordFindById__) and adds the 'request' and 'state'
data to the result.

 


