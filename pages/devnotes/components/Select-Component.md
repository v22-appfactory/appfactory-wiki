## Select Component

A custom Select component has been created to override some of the default behaviors in Formio.

### loadItems()
The select component overrides the loadItems call that accesses the service layer to get resources.  The change is to 
insert the resource key (GUUID) from this.component.resource into the url where it is expected by the REST API.
 
