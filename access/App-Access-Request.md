# Overview
The Appfactory application access processing has been designed to duplicate the VTAMP request process.  Users request
access to an application providing contact information, affiliations, desired role, and a reason for the access.  The 
request is then reviewed by an application administrator who can approve or reject the request.  Users that have not 
gotten CAC access are directed through the SAAR process and must complete that access and get approval prior to 
completing the application request.  Once a request is approved the user is given the approved role and can access the 
application based on the application role granted.

# Application Access Request
### AppAccessRequest Page
Navigation to the application access request page can be done in the navigation panel by clicking Administration / 
Application Access.  The page provides a list of the Applications that a user can choose from.  Once the user selects an
application and clicks Submit they are directed to the access request page.

NOTE:  If the user is not logged into the Appfactory they will be redirected to a login screen.  This is primarily an 
issue in the development or test environments.  How this will work in production has yet to be determined, but the issue
is whether the HTTP request has a NPKE_SUBJECT header.

### AccessRequest Page
The access request page allows the user to fill in user attributes, affiliation, activity, site, designation, branch,
rank/grade, desired role, and reason for access.  Attributes that are known for the user from their LDAP record or an
existing record in the Appfactory *users* table are filled in automatically.  After completing required fields and 
clicking Save Profile the following steps are taken:

* A *users* table record is updated for existing Appfactory users or created for new users using the information entered
in the accessrequest page.
* If the user does not have CAC access a record is created in the *saar_processing* table for tracking the SAAR process.
* A record is created in the *access_requests* table including the user id, desired role, reason, approver roles, and 
creation date.
* An email is sent to all users in the approver roles informing them of the application request.
* The user gets a success alert on the screen which they click to dismiss.
* Once the alert is dismissed the user is navigated to the Home page or the SAAR request page for non-CAC users.

# SAAR Processing and Review
### AccessRequestSaar Page
Users that must complete the SAAR process for CAC access will be redirected to this page when attempting to navigate to
any page other than the Home or Support pages.  The page contains checkboxes which should be updated as the user 
completes the steps in the SAAR process.  Once all four checkboxes are checked the Submit button is disabled.  When the
SAAR process is approved by an administrator this block is removed and the user can once again access the the 
application access request page.

### AccessReviewSaar Page
System and application administrators can review the existing SAAR requests using the access review SAAR page.  The 
SAAR requests are listed and the progress in the process are displayed.  The administrator can accept or reject the 
request in this list.  Once a request is approved or rejected it is removed from the list.


# Application Access Review
### AccessRview Page
System and application administrators review the application access requests on the Site Lead Actions (accessreview)
page.  The requests are listed and buttons are provided for edit, approve, and reject.  Clicking the approve or reject
buttons updates the access_requests record.  Clicking the edit button navigates to the New Access Request 
(accessrequestdetail) page which displayes more information about the request and allows the administrator to change the
role and add a note.  Buttons are provided to approve and reject the request.  The following actions occur:
* The access_requests record is updated for the decision
* A role assignment record is created giving the user the role.
* The user record *disabled* based on approval or rejection.

## Navigation to the access and SAAR review pages
### System Administrator
The system administrators have access to the review pages in the Administration node of the navigation menu:
* Administration / Access Review
* Administration / SAAR Review
### Application Administrator
Pages need to be added to the application for application administrators.  In the Test Application this has been done
by adding pages to the application Administration menu and can be accessed in the navigation panel:
* Test Application / Administration / Access Review
* Test Application / Administration / SAAR Review
### Dashboard
The user's dashboard can be set to one of the review pages providing an alternative navigation for that user.  This is
done by creating a record in the *dashboardreports* table 
 
## Testing
There is a notes.txt file which details the testing steps that have been used for tesing various scenarios:
appfactory-scripts/apps/accessrequest/notes.txt

The keycloak development users include three users for testing:
* tdod - user with *users* record and CAC access in the NPKE_SUBJECT string
* tnodod - user with *users* record and no CAC access in the NPKE_SUBJECT string
* tnorec - user without a *users* record

