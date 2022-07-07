# Reusable Maintenance Screens
Application lookup tables require screens that allow the application users to enter records for the application in 
common tables.  Appfactory has common tables that may be used by multiple applications.  The records for an application
are identified by the *appid* column allowing the table to persist records for different applications.  Common lookup
tables generally consist of the following columns:
* id - unique ID for the record
* appid - application ID
* label - the label used when showing the options for the lookup
* description - extended explanation of the record
* createdat - date and time of the record creation
* updatedat - date and time of the record last update
* jsondata - JSON column containing any additional columns being tracked in the table for an application

Tables that basically use the *id*, *appid*, *label*, and *description* columns can be maintained using the 
Administration __LookupTableMaint.vue__ screen.  This does require the user to have administrator role access.

Maintenance of a customized lookup table or maintenance of a lookup table in a page accessed by a non-system 
administrator can be done by creating a formio page using the FormBuilder.  This option is available to any application.
However, for any lookup table that uses a table's standard or common columns this cause unnecessary repitition where
the same page is being recreated over and over when the only difference in the records is the *appid* column value.
In order to address the need to replicate these screens, re-usable Vue pages can be made for common lookup tables.  The
pages address maintenance of specific tables and identify the application using the routing path used to navigate to the
page.  An example would be a workflow status maintenance screen in the test application which would have 
'/common/workflow/status/10' as a router path.  The '10' identifies that application as the Test Application.

Example common screens have been made for the four workflow tables and are in the *appfactory* project in the 
/src/views/appmaint/common directory:
* WorkflowStatus.vue - workflow status table : workflow_status
* WorkflowAction.vue - workflow actions table : workflow_actions
* WorkflowState.vue - workflow state table : workflow_states
* WorkflowStateTransition.vue - workflow state transitions table : workflow_statetransitions

The screens use common logic found in the commonMaintHelper.js module.  The key difference in the Vue pages are support
for the different columns or fields in the table and the need to load the options for any referenced tables.  An example
is the WorkflowStateTransition.vue which has select controls for:
* Roles - roles table
* State In - workflow_states table
* State Out - workflow_states table
* Action - workflow_actions table

The common screens use endpoints in the appdataController to handle the CRUD for the table being maintained:
```javascript
appdataRoutes.get('/record/:apptableId/:recordId', authController.authCheckUserRoles, controller.appdataRecordFindById);
appdataRoutes.post('/record/:apptableId', authController.authCheckUserRoles, controller.appdataRecordAdd);
appdataRoutes.put('/record/:apptableId/:recordId', authController.authCheckUserRoles, controller.appdataRecordUpdate);
appdataRoutes.delete(
'/record/:apptableId/:recordId', authController.authCheckUserRoles, controller.appdataRecordDelete);
```
All URLs start with appdata: 
```javascript
GET /appdata/record/:apptableId/:recordId

```

### Page Routing
Each common maintenance screen must be added to the __appfactory__ application router.js allowing the UI application to
navigate to the page.  An example of the routing definition for the workflow state page follows: 
```javascript
    {
      path: '/common/workflow/state/:appid',
      name: 'workflowstate',
      beforeEnter: guard,
      component: require('./views/appmaint/common/WorkflowState.vue').default
    },
```
Logic for special handling of the page also needs to added to the __services__ menuController.getRoutingPath method in
order for the router URL to be overridden when creating the navigation link.  This is illustrated below in the 
'routerpath' section.

### Application Table Definition
In order for the maintenance page to find the correct __apptables__ virtual table for the table being maintained and any
referenced tables, the tables involved need to be defined as application tables using the TableMaint screen.  This is
true whether a common maintenance screen or a custom formio page is used.
Using the WorkflowStateTransition example above this requires __apptables__ records for the tables:
* workflow_statetransitions
* roles
* workflow_states
* workflow_actions

### Adding a Common Maintenance Screen to an Application
There are several steps that are required to add a common screen to an application's pages and navigation menu.

#### menuitems Record needs a routerpath
When creating a page, the page can be added to the navigation menu.  At that time a value can be added to the menuitems
record which changes the router path for the menu item.  The *routerpath* value must be an exact match for the values 
supported in the menuController.getRoutingPath logic which searches for specific *routerpath* values and changes the
routing URL that is generated for the navigation menu item.  It basically overrides the standard '/apps/:appId/:pageID'
routing URL that would be assigned to the page.  A section of the logic follows:
```javascript
    switch(item.routerpath) {
      case 'adhoc':
      case 'reportbuilder':
      case 'simplequery':
      case 'subtasks':
      case 'accessreview':
      case 'accessreviewsaar':
        return `/${item.routerpath}/${item.appid}/${item.pageid}`;
      case 'workflowstatus':
      case 'workflowaction':
      case 'workflowstate':
      case 'workflowstatetrans':
        const str = item.routerpath.replace('workflow', '');
        return `/common/workflow/${str}/${item.appid}`;
      default:
        return `/apps/${item.appid}/${item.pageid}`;
    }
```
An example of the __menuitems__ table records:   
[[/images/common pages/menuitems_workflow_records.png|menuitems workflow records]]

When a page exists, but has not been added to the navigation menu (no menuitems record exists) two elements of the Page
Maintenance screen appear differently:
* The 'Add to Menu' button is enabled allowiing the page to be added to the navigation menu
* The 'Router Path' field appears and can be edited    
[[/images/common pages/page maint when adding to menu.png|PageMaint screen when adding to menu]]    
__*NOTE:*__ The reason that the 'Router Path' field only appears when adding an existing page to the navigation menu is
due to the fact that it is a column in the __menuitems__ table and the record is created at this time.    
__*TODO:*__ <span style="color: red;">make the menuitems record editable in the UI</span>

#### routerpages Record 
Records in the __routerpages__ table link router paths to __pages__ records in order to retrieve page access data in
the authController.authPage method.  
                                 
The __routerpages__ table records:        
[[/images/common pages/routerpages_records.png|routerpages records]]    
<span style="color: green;">Issue #29 Reuse of maintenance screens requires a routepages record to allow access to the page</span>    
__*TODO:*__ <span style="color: red;">review alternative ways to retrieve page access information</span>    
__*TODO:*__ <span style="color: red;">provide UI means for maintaining the routerpages table</span>


