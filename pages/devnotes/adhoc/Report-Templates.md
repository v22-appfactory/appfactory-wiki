## Workflow History Template
This sample template has a primary table [Workflow History] and four related tables:
* Work Request
* Workflow Actions
* Workflow States : starting state
* Workflow States : ending state

__Work Request History Template : Table Relationships__  
[[/images/adhoc/report-builder/work request history tables.png|Work Request History Table Relationships]]

__Work Request History Template : Template JSON and Attribute Values__  
[[/images/adhoc/report-builder/work request history template.png|Work Request History Template]]


## Template Attributes
Report Templates consist of a list of tables and table columns.  The attributes provide table reference information 
that allow queries to link records based on table relationships.  The template also defines a default set of columns
that will be displayed and the column orders.  The default column selections and order can be overridden when
specifying the query.  Any column in the template can be included in the query.

#### Table Attributes
* __id__ - the table ID
* ___comment__ - a name describing the table
* __related__ - a column ID that is used to link this table's ID to the specified column in the primary table 

#### Table Column Attributes
* __id__ - the column ID
* __label__ - label used when displaying the column in the report query screen
* ___comment__ - a name describing the column
* __displayorder__ - the order that the column will appear in the default column selection list or 0 if not displayed by
default
 