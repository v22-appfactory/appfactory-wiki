# Email Details 

### Overview
The delivery of emails is handled by configuring a __Server Action__ which is associated with a server call to a 
specified URL.  The server action can specify the _Method_ (GET, PUT, POST, DELETE) and whether the action should occur 
_Pre_ or _Post_ after the URL processing is done.  In the case of an email this will generally be done Post processing 
in order to use data that results from the URL processing.  The action also provides for the specification of _Action 
Data_ and a _Template_ for mapping the data used onto the template.  The following screen shot show an example of the
configuration of an email after processing a workflow update:
[[/images/email/server action for email.png|Server Action configuration for Email]]   

### Email _To_ List
Currently the email addressee or 'To' list is derived from a Notifications table that links user roles to a 
statetransitionid for the update of an issue in a workflow.  This implementation was based on the processing in the 
VTAMP application.  The current implementation will work when emails are sent to update users on updates to an issue in 
a workflow, but additional capabilities may be needed for other situations.

__NOTE:  Changes can be made to the email Server Action processing once additional requirements are provided.__

The current logic for creating emails starts in the actions.js module's _processAction_ method.  When processing an
email action a call is made to the RoleController.transitionNotificationUsers passing an object containing a 'tableId'
and 'transitionId' attributes which are obtained from the server action actionData.  The _transitionNotificationUsers_
method calls a _findTransitionNotificationsUsers_ database procedure which then calls a second procedure 
_findRolesByStateTransition_ that reads the specified table for records for the statetransitionid retrieving the 
specified user roles.  The _findTransitionNotificationUsers_ procedure then retrieves the users in the returned roles
by calling the _findRolesByStateTransition_ procedure.

1. __actions.processAction__ calls roleController.transitionNotificationsUsers({ tableId: 122, transitionId: 146})
2. __roleController.transitionNotificationUsers__ calls procedure app.findTransitionNotificationUsers(122, 146)
3. __app.findTransitionNotificationUsers__ calls procedure app.findRolesByStateTransition(122, 146)
4. __app.findRolesByStateTransition__ returns user roles specified in the table that match the transition ID    
__NOTE:__ The current implementation uses a custom table called Notifications which stores data in the app.appdata 
table.    
5. __app.findTransitionNotificationUsers__ calls procedure app.getUsersInRoles which returns a result set cotaining the
users in the specified roles.
6. __actions.processAction__ uses the list of users when specifying the send to attribute of the email.


