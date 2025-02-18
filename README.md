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
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")

var lastName = pm.variables.replaceIn("{{$randomLastName}}")

var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
// console.log(totalPrice)

var depo = pm.variables.replaceIn("{{$randomBoolean}}")
console.log(depo)
// console.log(firstName)

//DATE
const mnt = require('moment')
const today = mnt()
// console.log(today.add(1,'d').format('YYYY-MM-DD'))
var checkIn =  today.add(1,'d').format('YYYY-MM-DD')
var checkOut =  today.add(10,'d').add(1,'M').format('YYYY-MM-DD')

//additional needs
var need = ["Breakfast", "Lunch", "Snacks", "Dinner"]

//Math.random gives the float value betwwen 0 and 1
var needVal = Math.floor(Math.random()* need.length)
var addNeed = need[ needVal]
// console.log(needVal)
// console.log(addNeed)


pm.environment.set("first_name",firstName)
pm.environment.set("last_name",lastName)
pm.environment.set("totalPrice",totalPrice)
pm.environment.set("deposit_Paid",depo)
pm.environment.set("checkIn",checkIn)
pm.environment.set("checkOut",checkOut)
pm.environment.set("additionalNeed",addNeed)


```
 **Request Body:** 
 ```console 
 {
	"firstname" : "{{first_name}}",
	"lastname" : "{{last_name}}",
	"totalprice" : {{totalPrice}},
	"depositpaid" : {{deposit_Paid}},
	"bookingdates" : {
    	"checkin" : "{{checkIn}}",
    	"checkout" : "{{checkOut}}"
	},
	"additionalneeds" : "{{additionalNeed}}"
}
```
**Response Body:**
 ```console 
{
    "bookingid": 2944,
    "booking": {
        "firstname": "Marjory",
        "lastname": "Ritchie",
        "totalprice": 833,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2025-02-19",
            "checkout": "2025-04-01"
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
    "bookingid": 2944,
    "booking": {
        "firstname": "Marjory",
        "lastname": "Ritchie",
        "totalprice": 833,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2025-02-19",
            "checkout": "2025-04-01"
        },
        "additionalneeds": "Lunch"
    }
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
var updated_firstname = pm.variables.replaceIn("{{$randomFirstName}}")
var updated_lastname = pm.variables.replaceIn("{{$randomLastName}}")
var updated_price = pm.variables.replaceIn("{{$randomInt}}")
var updated_deposit = pm.variables.replaceIn("{{$randomBoolean}}")

//updated_DATE
const update_moment = require('moment')
const updated_today = update_moment()
// console.log(updated_today)

var updated_checkin = updated_today.add(2,'M').format("YYYY-MM-DD")
var updated_checkout = updated_today.add(5,'d').add(1,'Y').format("YYYY-MM-DD")

//additional need
var updated_need = ["Breakfast","Lunch","Snacks","Dinner"]
var updated_needval = Math.floor(Math.random()*updated_need.length)

var updated_addNeed = updated_need[updated_needval]

//environment_set
pm.environment.set("updated_firstname",updated_firstname)
pm.environment.set("updated_lastname",updated_lastname)
pm.environment.set("updated_price",updated_price)
pm.environment.set("updated_deposit",updated_deposit)
pm.environment.set("updated_checkin",updated_checkin)
pm.environment.set("updated_checkout",updated_checkout)
pm.environment.set("updated_aditionalneed",updated_addNeed)

```
  **Request Body:** 
 ```console
{
    "firstname": "Jeanne",
    "lastname": "Waters",
    "totalprice": 754,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2025-04-18",
        "checkout": "2026-04-23"
    },
    "additionalneeds": "Snacks"
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
![Image](https://github.com/Rupa-Dey/API_Testing_Project01.git/assets/72e80055-efba-457d-b1ca-da2329a15a74)
![Image](https://github.com/Rupa-Dey/API_Testing_Project01.git/assets/3d2f524a-ff92-48df-83b4-f9c99f642883)
![Image](https://github.com/Rupa-Dey/API_Testing_Project01.git/assets/5f89e4c7-ccfa-4ffd-8120-11a39e430a25)
![Image](https://github.com/Rupa-Dey/API_Testing_Project01.git/assets/effc564e-1dfb-44c6-be7e-0da7bca8faf0)
