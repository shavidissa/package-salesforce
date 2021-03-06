# Salesforce Connector

Salesforce connector provides a Ballerina API to access the 
[Salesforce REST API](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_what_is_rest_api.htm). 
It handles [OAuth2.0](http://tools.ietf.org/html/rfc6749), provides auto completion and type conversions.

## Compatibility

| Ballerina Version         | API Version |
| ------------------------- | ------------|
|   0.970.0-beta10           |   v37.0     |
 

## Getting started

1. Refer to [Getting Started guide](https://ballerina.io/learn/getting-started/) to download and install Ballerina.

2. Create a Salesforce account and create a connected app by visiting [Salesforce](https://www.salesforce.com) 
and obtain the following parameters:
* Base URl (Endpoint)
* Client Id
* Client Secret
* Access Token
* Refresh Token
* Refresh URL

IMPORTANT: This access token and refresh token can be used to make API requests on your own account's behalf. 
Do not share your access token, client secret with anyone.

Visit [here](https://help.salesforce.com/articleView?id=remoteaccess_authenticate_overview.htm) 
for more information on obtaining OAuth2 credentials.

3. Create a new Ballerina project by executing the following command.

      ``<PROJECT_ROOT_DIRECTORY>$ ballerina init``

4. Import the Salesforce package(sfdc37) to your Ballerina program as follows.

```ballerina

import wso2/sfdc37;

```

### Working with Salesforce REST connector.

All the actions return JSON or sfdc37:SalesforceConnectorError. If the action is a success, 
then result (non-empty) JSON will be returned while the sfdc37:SalesforceConnectorError will be null and vice-versa.

##### Example
 * Request

 ```ballerina
 import wso2/sfdc37 as sf;
 import ballerina/io;
 
 //User credentials to access Salesforce API
 string url = "<base_url>";
 string accessToken = "<access_token>";
 string refreshToken = "<refresh_token>";
 string clientId = "<client_id>";
 string clientSecret = "<client_secret>";
 string refreshUrl = "<refreshUrl>";
 
 
    public function main (string... args) {
        endpoint Client salesforceClient {
            baseUrl:url,
            clientConfig:{
                auth:{
                    scheme:"oauth",
                    accessToken:accessToken,
                    refreshToken:refreshToken,
                    clientId:clientId,
                    clientSecret:clientSecret,
                    refreshUrl:refreshUrl
                }
            }
        };
    
         //Call the Salesforce connector function getAvailableApiVersions().
        json|sf:SalesforceConnectorError response = salesforceClient -> getAvailableApiVersions();
            match response {
                //if successful, returns JSON result
                json jsonRes => {
                    io:println(jsonRes);
                }
        
                //if unsuccessful, returns an error of type sfdc37:SalesforceConnectorError
                sf:SalesforceConnectorError err => {
                    io:println(err);
                }
            }
    }
```
* Response

JSON response or SalesforceConnectorError struct
