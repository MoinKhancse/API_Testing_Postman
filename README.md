### **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:
https://documenter.getpostman.com/view/31254411/2sA35Bbj9D
  
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
  https://github.com/MoinKhancse/API_Testing/tree/main
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
3. Run Collection:
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
	var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
	pm.environment.set("firstName",firstName)
	
	var lastName = pm.variables.replaceIn("{{$randomLastName}}")
	pm.environment.set("lastName",lastName)
	
	var totalprice = pm.variables.replaceIn("{{$randomInt}}")
	pm.environment.set("totalprice",totalprice)
	
	var depositpaid = pm.variables.replaceIn("{{$randomBoolean}}")
	pm.environment.set("depositpaid",depositpaid)
	
	const date = require('moment')
	const today = date()
	//var cheekin = today.add(5,'d').format("YYYY-MM-DD")
	var checkin = today.format("YYYY-MM-DD")
	pm.environment.set("checkin",checkin)
	//var checkout = today.subtract(5,'d').format("YYYY-MM-DD")
	var checkout = today.add(3,'d').format("YYYY-MM-DD")
	pm.environment.set("checkout",checkout)
```
  **Request Body:** 
 ```console 
  {
	  "firstname" : "{{firstName}}",
	  "lastname" : "{{lastName}}",
	  "totalprice" : {{totalPrice}},
	  "depositpaid" : {{depositPaid}},
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
      "bookingid": 4334,
      "booking": {
          "firstname": "Joelle",
          "lastname": "Krajcik",
          "totalprice": 266,
          "depositpaid": true,
          "bookingdates": {
              "checkin": "2024-03-15",
              "checkout": "2024-03-20"
          },
          "additionalneeds": "Breakfast"
      }
  }
```
 ## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "D'angelo",
    "lastname": "Feeney",
    "totalprice": 757,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-03-15",
        "checkout": "2024-03-20"
    },
    "additionalneeds": "Breakfast"
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
    "token": "06eb798bf6f2caa"
}
```

 ## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
	var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
	pm.environment.set("firstName",firstName)

	var lastName = pm.variables.replaceIn("{{$randomLastName}}")
	pm.environment.set("lastName",lastName)
	
	var totalprice = pm.variables.replaceIn("{{$randomInt}}")
	pm.environment.set("totalprice",totalprice)
	
	var depositpaid = pm.variables.replaceIn("{{$randomBoolean}}")
	pm.environment.set("depositpaid",depositpaid)
    
    //Date
    	const date = require('moment')
	const today = date()
	//var cheekin = today.add(5,'d').format("YYYY-MM-DD")
	var checkin = today.format("YYYY-MM-DD")
	pm.environment.set("checkin",checkin)
	//var checkout = today.subtract(5,'d').format("YYYY-MM-DD")
	var checkout = today.add(3,'d').format("YYYY-MM-DD")
	pm.environment.set("checkout",checkout)
```
  **Request Body:** 
 ```console 
  {
	  "firstname" : "{{firstName}}",
	  "lastname" : "{{lastName}}",
	  "totalprice" : {{totalPrice}},
	  "depositpaid" : {{depositPaid}},
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
      "bookingid": 4334,
      "booking": {
          "firstname": "Joelle",
          "lastname": "Krajcik",
          "totalprice": 266,
          "depositpaid": true,
          "bookingdates": {
              "checkin": "2024-03-15",
              "checkout": "2024-03-20"
          },
          "additionalneeds": "monitor"
      }
  }
```

 ## _**5. Delete Booking Record**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Response Body: None 

## Run Command:  
- Run Command for Console: 
```console 
newman run Batch_24.postman_collection.json -e Batch_24.postman_environment.json  
```
- Run Command for Report: 
```console 
newman run Batch_24.postman_collection.json -e Batch_24.postman_environment.json -r cli,htmlextra
```

## Newman Report Summary:

![Screenshot 2023-06-04 234209](https://github.com/MoinKhancse/API_Testing/assets/137496247/fce9edcb-16b4-42bb-85a6-ef2f4d0f9989)

![Screenshot 2024-03-24 192625](https://github.com/MoinKhancse/API_Testing/assets/137496247/2605ab20-6649-4b8c-ae9b-33dff4d7457e)

![Screenshot 2024-03-24 192700](https://github.com/MoinKhancse/API_Testing/assets/137496247/6082a276-7abf-4d52-9462-e646f0df2bbc)

![Screenshot 2024-03-24 192737](https://github.com/MoinKhancse/API_Testing/assets/137496247/dc9c4533-a76b-482e-8099-77751490f50f)

![Screenshot 2024-03-24 192806](https://github.com/MoinKhancse/API_Testing/assets/137496247/e55652fa-a383-4625-abb1-9c7ec9d16726)




