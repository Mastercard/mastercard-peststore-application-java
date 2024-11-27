### Mastercard Petstore Application

Mastercard Petstore API
- API version: 1.0.0
- App version: 1.0.0

This application provides examples of how a Mastercard API should implement authentication, authorization, and payload encryption.
Please follow the steps in the documentation [here](https://developer.mastercard.com/reference-service-ngw/documentation)
to understand how to utilize this application and adapt it for your service.

## Requirements

Building the API client library requires:
1. Java 17+
2. Maven (3.8.3+)

## Installation

Please follow the instruction below to begin

```shell
mvn clean install
```

This will generate all required files as defined in [petstore.yaml](src/main/resources/petstore.yaml) using the [OpenAPI Generator](https://openapi-generator.tech/) plugin. They should be built into the target folder.

## Getting Started

Set properties in [application.properties](src/main/resources/application.properties)

The authentication mode (mTLS or OAuth1.0a) must be set by adding the following to your run command 
```
-Dspring.profiles.active=oauth
```
or
```
-Dspring.profiles.active=mtls
```
If using the API in OAuth1.0a mode the following are required in [application-oauth.properties](src/main/resources/application-oauth.properties)
```
mastercard.oauth.pkcs12KeyFile
mastercard.oauth.consumerKey
mastercard.oauth.keyAlias
mastercard.oauth.keyPassword
```
If using the API in mTLS mode the following are required in [application-mtls.properties](src/main/resources/application-mtls.properties)
```
mastercard.mtls.pfxKeyFile
mastercard.mtls.keyPassword
```
Encryption properties are required to be set. This API supports JWE encryption. This is in [application.properties](src/main/resources/application.properties)
```
mastercard.encryption.encryptionCert
mastercard.encryption.decryptionKeys
mastercard.encryption.decryptionKeyAlias
mastercard.encryption.decryptionKeyPassword
```

## Running the Application

To run the application use the command
```
mvn spring-boot:run
```
The will execute three scenarios covering all use cases

## Example Scenarios

Example scenarios can be found under [here](src/main/java/com/mastercard/app/petstore/examples)
There are provide simples uses cases, documented below

### Adoption Flow Example
This demonstrates the typical flow for an adoption. 
1) A new adoption is created 
2) The adoption is then retrieved using the adoption id from step 1 
3) Information is updated before removing it using the same id
4) Clean up. The adoption is removed from the system

### Employee Flow Example
This demonstrates the typical flow for managing an employee.
1) A new employee is added to the system
2) The employee's information is then searched for via SSN
3) Clean up. The employee is removed from the system

### Pet Flow Example
This demonstrates the typical flow for adding a new cat.
1) A new cat is added to the system
2) The cat's information is retrieved via it's id
3) That cat's status is updated to `RESERVED`
4) Clean up. The cat is removed from the system


## Support
For more information, please visit [https://developer.mastercard.com/support](https://developer.mastercard.com/support)

## Author

API_Consultancy_and_Standards@mastercard.com
