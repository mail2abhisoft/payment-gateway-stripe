# Getting Started

## Prerequisite

Java and Maven and MYSQL DB  has to be there before running this application.if not available then installed before proceeding next step.

## Technology Used

* Java 1.8
* Spring boot 2.6.4
* Mysql Database

## changes to the application code

* Create the account in Stripe and enable the API access and save your key seperatly.

* Generate self signed certificate for the application by running the below command on cmd

```json
keytool -genkeypair -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore das.p12 -validity 365

Enter keystore password:  <<enter any password>>
Re-enter new password:   <<reenter the same password>>
What is your first and last name?
  [Unknown]:  das
What is the name of your organizational unit?
  [Unknown]:  das
What is the name of your organization?
  [Unknown]:  das
What is the name of your City or Locality?
  [Unknown]:         
What is the name of your State or Province?
  [Unknown]:  
What is the two-letter country code for this unit?
  [Unknown]:  
Is CN=yong, OU=das, O=das, L=Unknown, ST=Unknown, C=Unknown correct?
  [no]:  yes
```

* Copy the 	das.p12 to the {project folder}/src/main/resources

* Goto SQL DB and run the below query 

```sql
create database orderdb;
```

* change the below properties in {project folder}/src/main/resources/application.properties

STRIPE_SECRET_KEY=**************** # use your account secret key generated in step -1
STRIPE_PUBLIC_KEY=**************** # use your account public key generated in step -1

spring.datasource.url = jdbc:mysql://localhost:3307/orderdb **# change the url and port **
spring.datasource.username = root  **## change user name **
spring.datasource.password = Password@1234 **## change password **
 
server.ssl.key-store=classpath:das.p12 **# change the file name according to certificate file name you copy in step 3 **
server.ssl.key-store-password=123456   **# change the password according to your keytool password**


### Steps to Build 

* Goto project folder and run **mvn clean install**

### Steps to run the application

* Goto project folder and run **mvn spring-boot:run**

### Test the application by enter the below url on browser

* https://localhost:8443

###Note : You can use either test key (or) live key ,but make sure while using the key you use you card according to key 
* example if you are using test key then use the 3d card based on your location to test the API 
	https://stripe.com/docs/testing
* Similarly if you use live key then use original 3d enable card to test the API .