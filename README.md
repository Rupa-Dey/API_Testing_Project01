### **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:
- https://documenter.getpostman.com/view/13082503/2sA2xmUAJ1
  
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
git clone  git@github.com:Rupa-Dey/API_Testing_Project01.git
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
2. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
3. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 

var firstname = pm.variables.replaceIn("{{$randomFirstName}}")
var lastname = pm.variables.replaceIn("{{$randomLastName}}")
var tot_price = pm.variables.replaceIn("{{$randomInt}}")
var depo_paid = pm.variables.replaceIn("{{$randomBoolean}}")

const momnt = require('moment')
const today = momnt()
 
var checkIn = today.add(1,'d').add(1,'m').format("YYYY-MM-DD")

var checkOut = today.add(10,'d').add(1,'m').format("YYYY-MM-DD")

var needs = ['Breakfast','Lunch', 'Snacks', 'Dinner']
var add_need = Math.floor(Math.random()*needs.length)

pm.environment.set("firstname",firstname)
pm.environment.set("lastname",lastname)
pm.environment.set("totalprice",tot_price)
pm.environment.set("depo_paid",depo_paid)
pm.environment.set("checkin",checkIn)
pm.environment.set("checkout",checkOut)
pm.environment.set("add_need",needs[add_need])

```
 **Request Body:** 
 ```console 
  {
	"firstname": "{{firstname}}",
	"lastname": "{{lastname}}",
	"totalprice": {{totalprice}},
	"depositpaid": {{depo_paid}},
	"bookingdates": {
    	"checkin": "{{checkin}}",
    	"checkout": "{{checkout}}"
	},
	"additionalneeds": "{{add_need}}"
}
```
**Response Body:**
 ```console 
{
    "bookingid": 3123,
    "booking": {
        "firstname": "Mertie",
        "lastname": "Harvey",
        "totalprice": 637,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2025-02-18",
            "checkout": "2025-02-28"
        },
        "additionalneeds": "Lunch"
    }
}
```
 ## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "Mertie",
    "lastname": "Harvey",
    "totalprice": 637,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-02-18",
        "checkout": "2025-02-28"
    },
    "additionalneeds": "Lunch"
}
```
## _**3. Create A Token For Authentication.**_
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
    "token": "0ee30d009a885d0"
}
```

 ## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 

var u_firstname = pm.variables.replaceIn("{{$randomFirstName}}")
var u_lastname = pm.variables.replaceIn("{{$randomLastName}}")
var u_tot_price = pm.variables.replaceIn("{{$randomInt}}")
var u_depo_paid = pm.variables.replaceIn("{{$randomBoolean}}")

const momnt = require('moment')
const today = momnt()
 
var u_checkIn = today.subtract(3,'d').add(1,'m').format("YYYY-MM-DD")

var u_checkOut = today.add(10,'d').add(1,'m').format("YYYY-MM-DD")

var u_needs = ['Breakfast','Lunch', 'Snacks', 'Dinner']
var u_add_need = Math.floor(Math.random()*u_needs.length)

pm.environment.set("ufirstname",u_firstname)
pm.environment.set("ulastname",u_lastname)
pm.environment.set("utotalprice",u_tot_price)
pm.environment.set("udepo_paid",u_depo_paid)
pm.environment.set("ucheckin",u_checkIn)
pm.environment.set("ucheckout",u_checkOut)
pm.environment.set("uadd_need",u_needs[u_add_need])
```
  **Request Body:** 
 ```console
{
    "firstname": "Magali",
    "lastname": "Jacobson",
    "totalprice": 662,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2025-02-14",
        "checkout": "2025-02-24"
    },
    "additionalneeds": "Dinner"
}
```
## _**5. Delete Booking Record**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Response Body: None 

## Run Command:  
- Run Command for Console: 
```console 
newman run API_CRUD_Testing.postman_collection.json -e API_CRUD_Testing.postman_environment.json
```
- Run Command for Report: 
```console 
newman run API_CRUD_Testing.postman_collection.json -e API_CRUD_Testing.postman_environment.json -r cli,htmlextra
```
## Newman Report Summary:
![Newman Report Summary](git@github.com:Rupa-Dey/API_Testing_Project01.git/newman/summary.png)


