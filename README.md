
# Restful API Testing with Postman and report with Newman 

This project showcases API testing with Postman, featuring a collection of tests to verify the functionality of various API endpoints.

## Features

- Comprehensive testing for GET, POST, PUT, and DELETE requests
- Well-structured test suite covering multiple API endpoints
- Configurable environment setup for seamless switching between different environments
- Pre-request scripts for dynamic data setup and test preparation
- Automated test scripts for assertions, validations, and response verification

### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
 ```console 
  git clone https://github.com/amzad1044/Testing-of-Rest-Api-with-Newman-Report.git
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman Html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```
### **Usage**
1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
2.  Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
8. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.
 
## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console
     var fName = pm.variables.replaceIn("{{$randomFirstName}}")
     pm.environment.set("firstName", fName)
     
     var lName = pm.environment.replaceIn("{{$randomLastName}}")
     pm.environment.set("lastName", lName)
     
     var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
     pm.environment.set("totalPrice", totalPrice)
     
     var d_paid = pm.variables.replaceIn("{{$randomBoolean}}")
     pm.environment.set("d_paid", d_paid)
     
     //Date
     const moment = require('moment')
     const today = moment()
     var checkin = today.add(5, 'd').format("YYYY-MM-DD")
     pm.environment.set("checkin", checkin)
     var checkout = today.add(10, 'd').format("YYYY-MM-DD")
     pm.environment.set("checkout", checkout)
```
### Post-response script:
```console
var jsonData = pm.response.json()
pm.environment.set("id", jsonData.bookingid)
```
**Request Body:**
```console
  {
  	"firstname" : "{{firstName}}",
  	"lastname" : "{{lastName}}",
  	"totalprice" : {{totalPrice}},
  	"depositpaid" : {{d_paid}},
  	"bookingdates" : {
      	"checkin" : "{{checkin}}",
      	"checkout" : "{{checkout}}"
  	},
  	"additionalneeds" : "Breakfast"
  }
```
**Response Body:**
```console
    {
        "bookingid": 3867,
        "booking": {
            "firstname": "Katheryn",
            "lastname": "Brekke",
            "totalprice": 27,
            "depositpaid": true,
            "bookingdates": {
                "checkin": "2025-02-12",
                "checkout": "2025-02-22"
            },
            "additionalneeds": "Breakfast"
        }
    }
```
## _**2. Get Booking information By ID**_

```console
   {
       "firstname": "Katheryn",
       "lastname": "Brekke",
       "totalprice": 27,
       "depositpaid": true,
       "bookingdates": {
           "checkin": "2025-02-12",
           "checkout": "2025-02-22"
       },
       "additionalneeds": "Breakfast"
   }
```
## _**3. Make A Token For Auth.**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script: None
### Request Body:

```console 
  {
  	"username": "admin",
  	"password": "password123"
  }
```
 **Response Body:**
  ```console 
    {
        "token": "fe95044713b7b05"
    }
  ```
## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console
  var fname = pm.variables.replaceIn("{{$randomFirstName}}")
  pm.environment.set("updatefirstName", fname)
  
  var lname = pm.variables.replaceIn("{{$randomLastName}}")
  pm.environment.set("updatelastName", lname)
  var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
  pm.environment.set("updatetotalPrice", totalPrice)
  
  var d_paid = pm.variables.replaceIn("{{$randomBoolean}}")
  pm.environment.set("updated_paid", d_paid)
  
  //Date
  const moment = require('moment')
  const today = moment()
  
  var checkin = today.add(5, 'd').format("YYYY-MM-DD")
  pm.environment.set("updatecheckin", checkin)
  var checkout = today.add(10, 'd').format("YYYY-MM-DD")
  pm.environment.set("updatecheckout", checkout)

```
**Request Body:** 
 ```console
{
	"firstname" : "{{updatefirstName}}",
	"lastname" : "{{updatelastName}}",
	"totalprice" : {{updatetotalPrice}},
	"depositpaid" : {{updated_paid}},
	"bookingdates" : {
    	"checkin" : "{{updatecheckin}}",
    	"checkout" : "{{updatecheckout}}"
	},
	"additionalneeds" : "Dinner"
}
```
**Response Body:**
 ```console 
{
    "firstname": "Jeffrey",
    "lastname": "Baumbach",
    "totalprice": 439,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-02-12",
        "checkout": "2025-02-22"
    },
    "additionalneeds": "Dinner"
}
```
 ## _**5. Delete Booking Information**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Response Body: None 

## Run Command:  
- Run Command for Report: 
```console
newman run Crud_ApiTesting.postman_collection.json -e Crud_ApiTesting.postman_environment.json -r cli,htmlextra
```
## Report Summary made by Newman:
![image](https://github.com/user-attachments/assets/a41921ff-c6af-47d9-92d5-da33014b71e1)
![image](https://github.com/user-attachments/assets/44151fe4-0472-4534-8dfd-bc08babb70ec)
![image](https://github.com/user-attachments/assets/cab380f3-b657-46e1-9901-0e7a03ea530b)
![image](https://github.com/user-attachments/assets/6cdbc1ac-7996-409f-a735-3608c3be2eab)




 
