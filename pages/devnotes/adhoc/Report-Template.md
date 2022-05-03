# Report Builder Templates

## Overview

_TBD_

## Report Templates Table [app.reporttemplates]
### Columns
1. id - primary key for the template
2. appid - application ID
3. createdat - creation date
4. upodatedat - last update date
5. primarytableid - apptables ID for the primary lookup table (currently not used)
6. jsondata - JSON report data model configuration

### JSONDATA
* Tables [Array] - array of tables in the report data model.  The first table listed is the primary lookup table  
  * id [Integer] - apptables.id  
  * _comment [String] - comment providing table information   
  * relatedto [Integer] - appcolumns ID of the data model primary table column that is the foreign key for this table   
  * columns [Array] - array of table columns to be included in the report data model   
    * id [Integer] - appcolumns ID
    * label [String] - column label that will be displayed to the user
    * _comment [String] - comment for indicating the table column
    * displayorder [Integer] - column position for the default results; 0 is used for columns not in the default results
    * linkColumn [String] - name of the foreign key column in the related table  
    NOTE: linkColumn could be derived from the relatedto column ID; the question would be where to capture this information     
 
#### Columns References
Columns that are not in the primary lookup table need to be populated by referencing other data in the query.  This needs
to be defined in the template in order to build the SQL for the query on the server.  In addition it is possible that
a foriegn key may be used twice in the query.  An example would be in a workflow state transition record that may 
reference the workflow state table twice, once for the 'statein' and once for the 'stateout' of the transition.  This
requires that the results display the state label column twice providing the labels for each state.

[[/images/adhoc/report-builder/state-transition-states-in-and-out.png|Example of report with multiple references.]]
 
