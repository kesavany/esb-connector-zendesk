﻿## Integration tests for WSO2 ESB Zendesk connector

### Pre-requisites:

 - Maven 3.x
 - Java 1.8
 - The org.wso2.esb.integration.integration-base project is required. The test suite has been configured to download this project automatically. If the automatic download fails, download the following project and compile it using the mvn clean install command to update your local repository:
		https://github.com/wso2-extensions/esb-connector-integrationbase

### Tested Platform:

 - UBUNTU 16.04
 - WSO2 EI 6.3.0
 - Java 1.8
 
### Steps to follow in setting integration test.

 1. Create a Zendesk account and get user credentials according to below steps:

	    i)  Navigate to URL "https://www.zendesk.com/register#getstarted" and create a trial account. 
	        (Save the given username[email address], password.)
	    ii) Once you registered it automatically navigates to "https://{company}.zendesk.com/agent/launchpad/configureEmailV2".
		    (Note the apiURl for further use. "https://{company}.zendesk.com" )
	    iii) When you send the request you have to save username, password and API URL.
	    iv)  Go to Admin > Channels > API and enable the Password Access.
 
 2. Download the WSO2 EI.

 3. Deploy relevant patches, if applicable.
 
 4. Follow the below mentioned steps for adding valid certificate to access Zendesk API over https

	    i) Extract the certificate from browser by navigating to apiUrl[Step 1->(iii)] and place the certificate file in following location.
	   "{ZENDESK_CONNECTOR_HOME}/src/repository"

 5. Update the 'esb-connector-zendesk.properties' file at the location "{ZENDESK_CONNECTOR_HOME}/repository" as below

        i)    apiUrl                     -		Use the api url, step 1->(iii)
        ii)   username                   -		Use the username, step 1->(iii)
        iii)  password                   -		Use the password, step 1->(iii)

 6. Following are the properties used in the 'esb-connector-zendesk.properties' file and 'zendesk.properties' file (in {ZENDESK_CONNECTOR_HOME}/src/test/resources/artifacts/EI/connector/config/) to run the integration tests.
 
        i)    apiUrl                     -		The api url.
	    ii)   username                   -		The username.
	    iii)  password                   -		The password.
	    iv)   fileName                   -		The file name of the file to upload with mandatory parameters.
	    v)    fileContentType            -		The content type of the file upload with mandatory parameters.
	    vi)   fileNameOptional           -		The file name of the file upload with optional parameters.
	    vii)  fileContentTypeOptional    -		The content type of the file upload with optional parameters.
	    viii) invalidApiUrl              -		An invalid api Url for apiUrl to list tickets and list tickets for recent with negative parameters.
	    ix)   query                      -		A query String for query to search tickets with mandatory/optional and negative parameters.
	    x)    componentType              -		A valid String value for the component type(tickets,topics,organizations,users) to add tags with mandatory/optional and negative parameters.
	    xi)   tag                        -		A String for tag to add tags with optional and negative parameters.
	    xii)  timeOut                    -		The time in milliseconds.
	    xiii) dueAt                      -		The task due date (format: yyyy-mm-dd) to create ticket with optional parameters.
	    xvi)  dueAtOptional              -		The task due date (format: yyyy-mm-dd) to update ticket with optional parameters.
	 
 6. Navigate to "{Connector_Home}/" and run the following command.<br/>
      ```$ mvn clean install -Dskip-tests=false```
