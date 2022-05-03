# Application Testing

## Vulnerability Testing

### REST API 
OWASP ZAP is currently being used as a means to run vulnerability tests against the REST API.  The tests are performed
by first logging into the application and then running various tests against the API endpoints.  When testing the API 
it is necessary to provide ZAP with a list of endpoints and provide information regarding how data is passed to the 
service endpoint.  This is done using OpenApi descriptions of the endpoints and then manually specifying parameters and
body data to replace using Fuzzing tests.

#### OpenApi

#### Running Attacks in ZAP
The steps for authenticating and running attacks against the endpoints is described in:  
[OWASP ZAP Testing Notes](Rest-Api-Zap-Testing "OWASP ZAP Testing Notes")
