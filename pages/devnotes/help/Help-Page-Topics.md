Help information for applications pages consists of three steps:

1. Create the help page in the wiki using markdown formatting.
2. Run a script to render the wiki .MD file into a HTML file and place the output in a directory available to the 
services application.
3. Update the __Pages__ table in the database setting the _helppath_ column value to point to the HTML file.

__Example:__   
* File location on the services server: /Volumes/help/sample application/administration/Damage-Cause-Maint.html
* Value in _helppath_ column: /sample application/administration/Damage-Cause-Maint.html
* Environment variable for help content path: __APPFACTORY_HELP_PATH=/Users/gmarshall/docker/volumes/help__ 

The Help menu item will appear for those menuitem/pages that have a value in the Page.helppath column.  If the 
Page.helppath column value is set to \<null> then the Help menu item will be hidden.

__NOTE:__ It is best to make the help content for a page as granular as possible.  The help content is displayed at the 
top of the page so succinct information without images is probably the most helpful when explaining how to input 
information in the page's form.  More elaborate information regarding an application can be provided on other pages 
within the Wiki.
 
### Running the script
The script is located in the services project: scripts/help/markdownDirectory.js and takes 3 parameters:
1. Source - the directory of the .MD files
2. Dest - the base help directory or __APPFACTORY_HELP_PATH__
3. Directory - the base directory of the files, both source and destination.  The source directory will be walked to 
get all files and subdirectories.
