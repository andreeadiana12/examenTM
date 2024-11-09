<h1>API Testing Project for https://reqres.in/api/ </h1>

The scope of this project is to use all  API knowledge gained throught the Software Testing course and apply them in practice, using a live application.

Application under test: **https://reqres.in/api/**

Tools used: Postman

<h2>Tests performed</h2>

<ol>
<li>**GET request**</li>

HTTP method for request: **GET**<br>
  Request description: **Used to request data from a server. It does not modify the resources on the server, it just reads them. It is used to get information, for example to see the list of users, details about a particular product, etc. In my case, I wanted to get a list of users on page 2.**<br>
Test types / techniques used: **Functionality, integration testing, limit testing**<br>
Response status code: **Response code: 200 OK**<br>

Below you can find a picture of the API request from Postman:<br>

**![image](https://github.com/user-attachments/assets/52908c1a-88ac-4dc9-b499-3867e5d25b63)**<br>

JavaScript Tests:

**![image](https://github.com/user-attachments/assets/e67e3c9f-6010-48c3-9596-08856619260e)**<br>


<li>**POST request**</li>

HTTP method for request: **POST**<br>
Request description: **Used to send data to the server to create a new resource. For example, submitting a user registration form. In my case, I wanted to create a new user with the name "Andreea" and the job "lawyer".**<br>
Test types / techniques used: **Functionality, validation testing, error testing, integration testing**<br>
Response status code: **Code response: 201 Created**<br>

Below you can find a picture of the API request from Postman:<br>

**![image](https://github.com/user-attachments/assets/818ecf08-0d16-4379-916f-4978f8994b73)**<br>

JavaScript Tests:

**![image](https://github.com/user-attachments/assets/07378882-777c-4fc6-84eb-515c3f5ddb3c)**<br>


<li>**PUT request**</li>

HTTP method for request: **PUT**<br>
Request description: **Used to update an existing resource on the server. It usually requires to submit all the necessary data to completely replace the resource. In my case, I wanted to update completely the user with ID 2.**<br>
Test types / techniques used: **Functionalitate, testare de validare, testare de regresie, testare a erorilor**<br>
Response status code: **Code response: 200 OK**<br>

Below you can find a picture of the API request from Postman:<br>

**![image](https://github.com/user-attachments/assets/dc64d150-34b4-42a7-a04f-e0ee658fb0c5)**<br>

JavaScript Tests:

**![image](https://github.com/user-attachments/assets/a1fd18e4-c461-437e-9ff1-3d7f06bca292)**<br>

</ol>

<h2>Execution report for the created API collection </h2>

Below you can find the execution report that was generated through the Postman collection runner. <br>

**![image](https://github.com/user-attachments/assets/0e471d6a-8456-4228-a2a6-cc03457fddf8)**<br>

<h2>Defects found</h2>

The following issues were identified while running the postman tests:<br>

<h2>Bug 1</h2>

**![image](https://github.com/user-attachments/assets/836c62d5-bc1e-4c13-b28a-37f36bb60bcd)**

**Description:** The POST endpoint does not return a proper error message when sending an empty request body. <br>
**Reproduction Step:** POST request to https://reqres.in/api/users without including a body. <br>
**Expected Result:** 400 Bad Request error response with a message indicating that the body is required. <br>
**Actual Result:** 201 Created response, suggesting that the user has been created, even though no data has been supplied. <br>
**Severity:** High (this may result in invalid users being created). <br>

<h2>Bug 2</h2>

**![image](https://github.com/user-attachments/assets/286dc549-80cb-47e6-b650-b87c944fb5db)**

**Description:** The PUT endpoint returns a successful response even when sending a user ID that does not exist in the database. <br>
**Reproduction Step:** Request PUT to https://reqres.in/api/users/9999 with a valid body: {"name":"Test User", "job":"Tester"}. <br>
**Expected Result:** 404 Not Found error response, indicating that the user with ID 9999 does not exist. <br>
**Actual Result:** 200 OK response, with a success message, suggesting that the user has been updated, even though the ID does not exist. <br>
**Severity:** High (this bug can be confusing and allows changes for users that do not exist). <br>

<h2>Conclusions</h2>

Total tests performed: **6 tests** <br>
Percentage of requests covered: <br>
- Total requests: 3 (GET, POST, PUT) <br>
- Tests performed per request: 2 for each type <br>
- Coverage percentage: (6 tests performed / 3 request types) * 100 = **200%** <br>
Remark: This shows that each request type was tested multiple times, allowing a more complete evaluation of functionality. <br>
Percentage of tests passed: <br>
- Tests passed: 4 (GET and POST passed all tests, but PUT had a non-existent ID issue) <br>
- Tests failed: 2 (one of the PUT tests and one of the POST tests) <br>
Percentage of tests passed: (4 tests passed / 6 tests performed) * 100 = **66.67%** <br>
Risk of launching the application without fixing bugs: <br>
- Bugs identified: <br>
-> Bug 1 (POST not validating data correctly) - **high severity** <br>
-> Bug 2 (PUT returning a successful response for non-existent IDs) - **high severity** <br>
Risk assessment: <br>
**Due to the high severity of reported bugs , there is a significant risk of launching the application without fixing these issues. An user may create invalid data or update a user that does not exist, which could lead to confusion and errors in the application.**
