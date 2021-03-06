#  Melrose Frontend Engineering Challange

## Overview:
The objective of this test is for you to showcase your frontend engineering skills and coding style.  Although this can be done with pure HTML and vanilla JavaScript, you are encouraged to use a framework such as React.js.  You can use whatever public packages/modules or personal libraries you have available to you.  If you'd prefer, you can use any library to bootstrap your project such as https://github.com/facebookincubator/create-react-app to speed up your setup.  

This test is not timed, but try to keep track of the amount of time you did spend on it, and include a comment in your main source file.  When you finish, please send the zipped solution to justin@theknollagency.com.  Please do not publish the solution to this test to any public repositories.

## Test:
You are tasked to build an admin page for a personnel management system.  You are given API endpoints described in the below section to complete your task.  The requirements are listed as follow:

1. Main page displays all people in the system, any simple view that shows at least their name and email address will do.  There's no need to perform any pagination on this page.
2. When a person's name is clicked, a modal should show up displaying their detailed information about the user, including the picture sized appropriated.  Assume all pictures have a 1:1 aspect ratio and are larger than 300x300px.
3. Make at least two textfields editable, and submit the result back to the server when the user submits.  Be sure not to allow submits if no content was changed.

## APIs:
API Base URL: https://melrose-frontend-challenge-api.us-west-2.elasticbeanstalk.com.  Please have your application get an access token from the `GET /v2/auth_token?email=:your_email_address` endpoint before calling any other apis.  The `access_token` returned from that is to be sent with all subsequent API calls as the `Authorization` header.

Although in this case, the `access_token` will not expire, please do not assume that behavior and prefetch that outside of your app.  You must get obtain that token at the start of your app.

Get Access Token
---
Return an access token to be used in subsequent API calls

* **URL**

`/v2/auth_token?email=:your_email_address`

* **Method:**

`GET`

*  **URL Params**

email: Your email address

None

* **Data Params**

None

* **Success Response:**

  * **Code:** 200 OK
  
  * **Content:** 
```json
{
    "message": "OK",
    "request_id": "f602dc5b-be44-485e-aea3-568577e839ed",
    "session_id": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.YWYwODg1YTYtNTIwMS00YWEwLWExYTYtZmY2MjFjMWU3MzZm.7faB9uCV9sXtVbAJoVJ_N6MXC1850fH90Cr0j-HCB4I",
    "data": {
        "access_token": "REDACTED"
    }
}
```

* **Error Response:**

  * **Code:** 401 Unauthorized
  * **Content:** 
```json
{
    "message": "unable to process request",
    "request_id": "e9e6d3e3-e855-46eb-b898-b0d6b95e3c3e",
    "session_id": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.YWYwODg1YTYtNTIwMS00YWEwLWExYTYtZmY2MjFjMWU3MzZm.7faB9uCV9sXtVbAJoVJ_N6MXC1850fH90Cr0j-HCB4I",
    "errors": [
        "An error has occured, please try again later"
    ]
}
```

Show All Persons
----
Returns json data about all persons.

* **URL**

`/v2/persons`

* **Method:**

`GET`

*  **URL Params**

None

* **Data Params**

None

* **Success Response:**

  * **Code:** 200 OK
  
  * **Content:** 
```json
{
"message": "OK",
"request_id": "b85b1c19-db64-49cb-bdcb-e8c60f51c004",
"session_id": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.YWYwODg1YTYtNTIwMS00YWEwLWExYTYtZmY2MjFjMWU3MzZm.7faB9uCV9sXtVbAJoVJ_N6MXC1850fH90Cr0j-HCB4I",
"data": [
        {
        "id": "5b0da33caecb4560240b9ec8",
        "first_name": "Doug",
        "last_name": "Smith",
        "email": "douggy@gmail.com",
        "photo": "https://static1.squarespace.com/static/5940a0d2725e257d7b398f81/t/598a7db0e3df28c8a47e690a/1502248386643/headshot-08-2.jpg?format=1500w",
        "phone_number": "",
        "birthday": "1983-01-05T00:00:00Z"
        },
        ...
]}
```

* **Error Response:**

  * **Code:** 500 Internal Server Error
  * **Content:** 
```json
  {
"message": "unable to process request",
"request_id": "13e1881f-72e2-493d-8f52-6843cc3440fc",
"session_id": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.YWYwODg1YTYtNTIwMS00YWEwLWExYTYtZmY2MjFjMWU3MzZm.7faB9uCV9sXtVbAJoVJ_N6MXC1850fH90Cr0j-HCB4I",
"errors": [
    "An error has occured, please try again later"
]}
```


Show One Person
----
Returns json data about a single person.

* **URL**

`/v2/person/:id`

* **Method:**

`GET`

*  **URL Params**

**Required:**

`id=[integer]`

* **Data Params**

None

* **Success Response:**

  * **Code:** 200 OK
  * 
**Content:** 

```json
{
  "message": "OK",
  "request_id": "b85b1c19-db64-49cb-bdcb-e8c60f51c004",
  "session_id": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.YWYwODg1YTYtNTIwMS00YWEwLWExYTYtZmY2MjFjMWU3MzZm.7faB9uCV9sXtVbAJoVJ_N6MXC1850fH90Cr0j-HCB4I",
  "data": 
    {
        "id": "5b0da33caecb4560240b9ec8",
        "first_name": "Doug",
        "last_name": "Smith",
        "email": "douggy@gmail.com",
        "photo": "https://static1.squarespace.com/static/5940a0d2725e257d7b398f81/t/598a7db0e3df28c8a47e690a/1502248386643/headshot-08-2.jpg?format=1500w",
        "phone_number": "",
        "birthday": "1983-01-05T00:00:00Z"
    }
}
```

* **Error Response:**

 * **Code:** 500 Internal Server Error
  * 
**Content:** 
```json
{
  "message": "unable to process request",
  "request_id": "724e51ce-7e93-4ed1-a221-0b93cc2aef80",
  "session_id": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.YWYwODg1YTYtNTIwMS00YWEwLWExYTYtZmY2MjFjMWU3MzZm.7faB9uCV9sXtVbAJoVJ_N6MXC1850fH90Cr0j-HCB4I",
  "errors": [
    "not found"
  ]
}
```


Edit One Persons
----
Edit a single person.

* **URL**

`/v2/person/:id`

* **Method:**

`PUT`

*  **URL Params**

  **Required:**

`id=[integer]`

* **Data Params**

Only submit fields that needs to be edited.  Available fields are `first_name`,`last_name`,`email`,`phone_number`
```json
{
  "first_name" : "Greatest",
  "last_name": "Ever",
  ...
}
```

* **Success Response:**

  * **Code:** 200 OK
  * **Content:** 
```json
{
  "message": "OK",
  "request_id": "9fd15aa0-0718-4eaf-ae98-22711d9e5252",
  "session_id": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.YWYwODg1YTYtNTIwMS00YWEwLWExYTYtZmY2MjFjMWU3MzZm.7faB9uCV9sXtVbAJoVJ_N6MXC1850fH90Cr0j-HCB4I"
}
```

* **Error Response:**

  * **Code:** 500 Internal Server Error
  * **Content:** 
```json
{
"message": "unable to process request",
"request_id": "6147259f-7e82-47a9-99ac-cdb4275c2a35",
"session_id": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.YWYwODg1YTYtNTIwMS00YWEwLWExYTYtZmY2MjFjMWU3MzZm.7faB9uCV9sXtVbAJoVJ_N6MXC1850fH90Cr0j-HCB4I",
"errors": [
    "invalid person id"
]}
```

