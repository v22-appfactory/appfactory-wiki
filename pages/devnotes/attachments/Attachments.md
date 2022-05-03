The following are notes regarding the attachment functionality and technical issues.

#### Processing Steps
1. Select one or more files in the form file upload component.  
    * File upload component calls /files/upload  
    * Database function _attachmentAddUpload_ is called    
        * creates __attachment__ record  
        * creates __userattachments__ record to link the attachment with the user  
    * Returns link to download the file from the uploads directory  
2. User submits the form with files selected in the file upload component  
    * appformController form add or form update functions are called  
    * After the form record is inserted/updated the __formController.updateAttachments__ is called  
        * The application directory is created if it does not exist  
        * The file is moved from the uploads directory to the application directory  
        * Database function _attachmentUpdate_ is called  
            * The __attachment.location__ is updated for the new location  
            * The __userattachments__ link is removed  
            * A __tableattachments__ link is created for the table/record being updated  
        * If there is a server action to save to a history file a __tableattachments__ link is created to the history
        record
  
#### Formio File Upload Component
File upload capability is added to a formio form by including a File Component and setting component attributes.  The
following attributes are of interest:
1. Display Tab
    * Multiple Values - required in order to process multiple uploads
2. File Tab
    * Storage -  select Url
    * Url - enter the url for the upload rest api [http://localhost:3000/files/upload]
    * Custom request options - add withCredential attribute
    `{ "withCredentials": true }`
    * API Tab - no Application/Category/Test Field Mapping is required because the attachments are not stored in a 
    column in the table but instead a link table is used   
__NOTE__: The Url attribute above is hard coded and should be replaced with a DNS name that can be redirected for the 
environment that is being targeted.   
[[/images/attachments/file-upload-component-file-dialog.png|File Upload Components File Dialog Attributes]]
    
#### REST API 
* POST /files/upload => uploadFiles() - stores file in uploads directory and links file to user
* GET  /files/temp/:fileName => downloadTempFile - route to retrieve a file stored in the uploads directory
* GET  /files/:appId/:fileName => downloadFile - route to retrieve an application file 
###### Controller Methods
* __uploadFiles__ - processes file in temporary uploads directory and creates __userattachments__ link
* __downloadTempFile__ - download a file in the uploads directory
* __downloadFile__ - download a file from an application directory
* __updateAttachments__ - moves file from the uploads directory to its application directory

#### Database Tables and Functions
* Tables
    * __attachments__ - The record of the file with a location, unique name, and original name
    * __userattachments__ - Link table for linking users and attachments
    * __tableattachments__ - Link table for a table/record and attachments
* Functions
    * _attachmentAddUpload_ - creates the __attachments__ record and the __userattachments__ link record  
    * _attachmentUpdate_ - updates the __attachments.location__, removes the __userattachments__ record, and creates the
    __tableattachments__ link record  
    * _attachmentAddLink_ - creates a __tableattachments__ link record (used for a History record)  
#### History Links
__NOTE__: Currently if a server action for a 'database' action is defined a link record will be created for the new record 
and each attachment found in the form being updated.  If this needs to be done selectively then an attribute can be 
added to the server action.
 
#### Initial Upload of Files and Reloading User Attachments
When a file is initially selected or dragged and dropped into the file upload component the file is upload to the 
server, stored in a temporary directory, and linked with the current user.  When the form is submitted the file is 
moved to the application directory and the file is linked to the form record.  If a user selects a file but leaves the
page without submitting the form the file remains in the temporary storage directory and linked to the user.  Whenever
a user views a form containing a file upload component any files that are linked to that user are relisted in the file
upload component.  The user can then submit the files associating them with a form record or delete them by clicking
the 'x' button displayed with the file.
[[/images/attachments/file-upload-component-list.png|File Upload Component With Files Listed]]    
__NOTE:__ When deleting uploaded attachments by clicking the 'x' button a REST call is made to the backend to remove
the attachment and the link to the user.  The filename link has a _href_ attribute that is provided by the server when
retrieving the attachment as the _url_ attribute in the JSON object.   

##### Reloading User Attachments in a Form
In order to reload existing linked files for a user it is necessary to add a _userattachments_ action for the form 
_load_ event.  The _action data_ for the event/action specifies the form file upload component name.  In the following
example the file upload component name is 'attachment':  
`{"component":"attachment"}`

