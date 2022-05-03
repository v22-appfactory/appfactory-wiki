#### DataTable List
A list of records in a table is shown using a Datatable that displays pages of records.  The datatable supports 
exporting, searching, paging, and record maintenance.  The number of records displayed can be changed and both the total
records    

##### Paging
The query that loads the table retrieves all records by default, but the number of records actually retrieved can be
restricted to a maximum records that is set for the whole system in order to prevent long retrieval times.  The user
can page through the records and the application will automatically query for additional records when the paging goes
beyond the number of records that have been previously retrieved.

##### Datatable Controls and Functions

###### Export
Results can be exported to PDF, Excel, CSV, Clipboard, or Printed.  If there are more records than the system maximum
then the exported results need to be saved on the server and retrieved by an system adminstrator.  Complete result sets
are exported to a file in a location specified by the user.
###### Search Column
A search column can be specified and any text searches will be limited to values in that column.
###### Search
Results can be filtered by specifying search text.  If no search column is specified then a match will be made on all
column values.  Large result sets (greater than the system maximum) must have a search column specified when searching.
###### Columns and Sorting
The table columns are listed in the top row.  Sorting can be done by clicking on the column name.  Clicking toggles
sorting between ascending, descending, and off.  Only single column sorting is currently supported.  
###### Rows per page
The number of rows per page can be changed by clicking the 'Rows per page' down arrown and selecting the number of rows
to display.  Choices are 5, 10, 15, and All.  Care should be taken when selecting All for large result sets as the
display rendering can take longer.
###### Rows displayed and total records
The set of records displayed and the total number of recores is shown to the right of the 'Rows per page' control.
###### Paging controls
Paging controls are VCR type controls for first, previous, next, and last.  For large result sets additonal queries may
be trigger when paging goes beyond the record set that is currently retrieved.  When querying the rows will clear and a
loading indicator will be shown until the query is complete.
###### Actions
When available the actions column has icons for editing and deleting a row.  The actions available are set for each
table by the application administrator.    

[[/images/appfactory/datatable/edit-icon.png|Edit Icon]]  Navigates to a record maintenance screen.   

[[/images/appfactory/datatable/delete-icon.png|Delete Icon]]  Allows the user to confirm and then delete the record.
  