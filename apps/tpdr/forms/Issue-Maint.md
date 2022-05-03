#### Issue Maintenance

##### Overview
The issue maintenance form allows the entry and editing of issues that are being tracked.  An issue can be 
of any type i.e., TPDR, EIR, TD/TCTO, etc.  Issues are tracked through workflow stages defined for the Issue
Type.

##### Fields
###### Driver ID
The ID used for the driver and how it is tracked.  Example: For a TPDR the driver ID would be the TPDR ID.
###### RCN
Report control number.
###### Driver Type
The driver type being tracked by this issue.
###### Priority
The priority or category associated with the driver being tracked.
###### Issue Type
The issue type specifies the workflow used to process the issue.  Issue types are specified for each driver type.  
NOTE: The options in the control are updated when the driver type is selected.
###### Rect
_TBD_
###### Created - Readonly in Edit Mode
The timestamp for when the issue was created.
###### Last Update - Readonly in Edit Mode
The last time the issue was updated.
###### Title
Title from the driver that is being tracked.  Example: TPDR title.
###### Author
Creator or owner of the issue.
###### Assignee
User that has been assigned the issue.
###### Int Status
Currently not supported.
###### Action - Shown in Edit Mode
Workflow action choices.  This field is used to change the workflow state of the issue.
###### Workflow State - Readonly in Edit Mode
Current workflow state.
###### Workflow Action - Readonly in Edit Mode
Last workflow action.
###### ID - Readonly in Edit Mode
Record ID of the issue being edited.

##### Attachments
Files can be attached to an issue.  The files are attached by selecting them in the 'Add Attachments' control
and are uploaded when the issue is submitted.  They are listed in the 'Attachments' field and can be removed.
An example file attachment would be the TPDR and/or TMSDR PDF files.  Attachments are viewed by clicking on
the file link in the 'Attachments' list.  The Attachments field is only shown in Edit Mode.
###### Remarks
Text field allowing the entry of remarks for the issue.  Additional remarks can be added during subsequent edits.

##### Buttons
###### Submit
Creates or updates the issue and navigates to the Issue List page.  When all required fields are entered the Submit 
button is enabled.
###### Cancel
Cancels or clears the input allowing new issues to be entered.
###### Defects
The Defects button is shown when editing an existing issue.

Clicking the 'Defects' button navigates to the Defects screen where defects can be entered for the Issue.  The Issue
Defects screen shows readonly fields for the current issue, editable fields for the defect, and a list of defects 
for the issue.  Issue defects are created by entering a Defect Code and Comment for the defect and clicking Submit.  
Existing defects are edited by clicking the edit Action for a defect in the Defects list, making changes, and then 
clicking Submit. 


