Server messages and User Interface (UI) messages are logged into files in the directory:
$APPFACTORY_VOLUMES_PATH/logs

There are currently two log files, one for Express (REST api) calls and one for application logging:
__REST:__ $APPFACTORY_VOLUMES_PATH/logs/appfactory-rest.log    
__Application:__ $APPFACTORY_VOLUMES_PATH/logs/appfactory-server.log

Logging messages are captured in a JSON format in order to capture as much data as possible and make parsing the logs
easier.  Note the following is formatted for clearity while the logs file messages are stored without the white space.
``` javascript
{
  "meta": {
    "req": {
      "url": "/menus",
      "headers": {
        "host": "localhost:3000",
        "connection": "keep-alive",
        "accept": "application/json",
        "origin": "http://localhost:8080",
        "user-agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36",
        "dnt": "1",
        "sec-fetch-mode": "cors",
        "sec-fetch-site": "same-site",
        "referer": "http://localhost:8080/",
        "accept-encoding": "gzip, deflate, br",
        "accept-language": "en-US,en;q=0.9",
        "cookie": "mysession=eyJwYXNzcG9ydCI6eyJ1c2VyIjozNTc1fX0=; mysession.sig=h-t5gK2g4CYR05jW55BuxKhKIGI"
      },
      "method": "GET",
      "httpVersion": "1.1",
      "originalUrl": "/menus",
      "query": {}
    },
    "res": {
      "statusCode": 200
    },
    "responseTime": 155
  },
  "level": "info",
  "message": "HTTP GET /menus",
  "timestamp": "2019-11-05 07:24:38"
}
```

#### DEV Logging
If the environment variable VUE_APP_MODE = DEV then log messages will also be sent to the console using selected 
attributes.  The log messages will shown in an conventional format.
``` javascript
info: GET /adhoc/templates/queries/10 status: 304 33ms @ 2019-11-06T15:55:20.303Z
```

### Viewing
Currently the JSON files must be converted into a more easily viewed format using a command line tool.  In the future
log aggregation can be done using an open source tool such as Splunk, ELK (Elasticsearch, Logstash, and Kibana), 
Logstash, Fluentd, Papertrail, Graylog, Loggly.

#### Command Line Tool - JQ
The jq tool is a sed like tool that will parse a JSON file and filter results.  It can also be used to export results 
to CSV for viewing in Excel.  There are versions for MacOS, Windows, and Linux.
https://stedolan.github.io/jq/

Example uses:

Filter the appfactory-server.log retrieving only the 'level', 'message', and 'timestamp' from each entry:
``` javascript
cat ~/docker/volumes/logs/appfactory-server.log  | jq -r '[.level, .message, .timestamp]'
```

Export to CSV:
``` javascript
 cat ~/docker/volumes/logs/appfactory-server.log  | jq -r '[.level, .message, .timestamp] | @csv'
```
  
