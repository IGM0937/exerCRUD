# exerCRUD

Small repository containing a small exercise specifications for creating a new CRUD REST API project.

- [Overview](#overview)
  - [Recommended research](#recommended_research)
  - [Recommended prerequisites](#recommended-prerequisites)
- [Base Specification](#base-specification)
  - [Accounts](#accounts)
  - [Purchases](#purchases)
  - [Settlements](#settlements)
- [Extra CRUD_bank features](#extra-crud_bank-features)
  - [Interest](#interest)
  - [User Credentials](#user-credentials)
  - [API Authentication](#api-authentication)
  - [Reporting](#reporting)

## Overview

The example specification looks to create a CRUD REST API project for a example credit card provider, CRUD_bank.

The following specification is used for new comers to the world of Software Engineering 🌍 🖥️

### Recommended research

The following questions are not necessary to answer before starting, but may help you with development.

Most of these can be looked at as and when needed.

- What is REST API?
- What is JSON formatting and what is it used for?
- What is CRUD?
- What are the available HTTP codes in a typical REST API?
- What is a relational database?
- What is Docker?

### Recommended prerequisites 

Before starting the project, think about some baseline questions:

- What language are you looking to use? 
- What database are you going to utilise?
  - Will it be relational? NoSQL?
- What utility will you use to send API requests and see the responses?
  - Will it be another service application all together?

Here are some baseline recommendations:

- Select a good IDE
  - VSCode is popular and versatile at the time of writing.
  - JetBrains line of community products (the ones that are free).
  - If you want to be a 10x giga-chad developer, use Neovim or Emacs (not recommended for beginners). 
- Use Docker containers to easily setup your database instance.
  - Do look into data persistency. There are some docker containers that will remove your data once you turn off the containers.
  - Recommend looking into relational databases like SQLite and Postgres.
- Utilise existing and trusted open source libraries for:
  - Any HTTP server creation for your API endpoints.
  - Any connections to a database of your choice.
- For API utilities, you can use Postman, Insomnia, Hoppscotch, Milkman or even some plugins that come built into IDE

Majority of the recommendation will require some research just any of the above information is out of date.

## Base Specification

The following section will provide the very basics of the project to get you started.

### Accounts

#### Create User

The ability to create a user who has joined CRUD_bank.

Example Request:
```
POST http://localhost:8443/account/create
{
  "first_name": "Joe",
  "last_name": "Schmoe"
  "dob": "10/10/1991"
}
```

Example Response:
```
HTTP Code: OK 200
{
  "message": "Account for Joe Schmoe has been created. Account ID is 1"
}
```

#### Fetch User

The ability to fetch user information.

Example Request:
```
GET http://localhost:8443/account/1
{
  // no body
}
```

Example Response:
```
HTTP Code: OK 200
{
  "account_id": 1
  "first_name": "Joe",
  "last_name": "Schmoe"
  "dob": "10/10/1991"
}
```

#### Update User

The ability to update a user information.

Example Request:
```
PUT http://localhost:8443/account/1
{
  "first_name": "Jane",
  "last_name": "Doe"
  "dob": "11/11/1992"
}
```

Example Response:
```
HTTP Code: OK 200
{
  "message": "Account ID 1 has been updated."
}
```

#### Delete User

The ability to delete a user from the banks database.

Example Request:
```
DELETE http://localhost:8443/account/1
{
  // no body
}
```

Example Response:
```
HTTP Code: OK 200
{
  "message": "Account ID 1 has been deleted."
}
```

#### Questions and Extras

- What is the best way to store users information in a database?
  - Do you just use one table or do you separate the information out to separate tables and why?
- How do you generate a new account ID?
  - Do you use the primary key of a database?
  - Do you randomly generate a number when the user is created?
- For each endpoint, are there any validation you want to do on the incoming payloads?
  - e.g. Are all the expected fields available? If not, maybe send back an appropriate error response?
- For each endpoint, are there any validation you want to perform on the incoming data?
  - e.g. Is the coming date for date of birth formatted correctly?
  - e.g. Is the new user over the age of 16? 

### Purchases

Expand on the users account to have the ability to track costs and purchases.

#### Purchase

The ability for a user to make purchases.

Example Request:
```
POST http://localhost:8443/purchase
{
  "account_id": 1,
  "name": "Tesco shopping",
  "amount": 20.00
}
```

Example Response:
```
HTTP Code: OK 200
{
  "message": "Account ID 1 purchased Tesco shopping for £20.00"
}
```

#### Questions and Extras

- How will you represent the users account balance in the database?
- Will an account have a spending limit?
  - e.g. If so, what type of error responses do you want to show?
- Can the response message be expanded with useful information?
  - e.g. Could you inform the user of their latest credit card allowance and limits?

### Settlements

The ability for a user to settle their credit card debt.

Example Request:
```
POST http://localhost:8443/settle
{
  "account_id": 1,
  "amount": 20.00
}
```

Example Response:
```
HTTP Code: OK 200
{
  "message": "Account ID 1 settled £20.00"
}
```

#### Questions and Extras

- Will an account be allowed to overpay their debt?
  - e.g. If so, then by how much?
  - (In the real word, credit card companies don't like people overpaying their debt, because they can't charge interest on those accounts!)

## Extra CRUD_bank features

Beyond the basic CRUD operations and features that would make an application a credit card themed, you can also include the following features for extra practice.

### Interest

Expand your applications to generate interest on all accounts so that CRUD_bank can make some money!

Start up a reoccurring scheduler (HINT: alongside or at the same time as you start up your HTTP server) to go though all accounts at some interval to add interest all account debt.

- How will you iterate though all your accounts?
- How exactly are you going to work out who is in debt and how to add interest?
- How often are you going to run this scheduler?

### User Credentials

Expand Account APIs ability to store and use user passwords

- Set a password when an account is being created.
  - Is there a password criteria that needs to be validated? (Minimum 6 characters, must contain a letter, etc..)
  - How are you going to store the account passwords?
  - (You can do clear text, but in the real world, a good practice is to encrypt your passwords when storing them into a database. See Salt and Hash)
- Expand the PUT call to have the ability to update the password.
- Expand Account Update, Account Delete, Purchases and Settlements to require the account password.


### API Authentication

Expand all of the APIs to utilise some form of authentication to validate the caller for an API.

This is different from an account password. The account password ensures that the account user calling the API is the right user, but the API authentication ensures that the utility , tool or another API that is calling your application is allowed to call your APIs.

- Will you use any existing libraries to do this?
- Have you considered JWT for example?
- If you wish to do it by yourself, how are you going to generate a authorisation token?
  - What new endpoints do you have to create to generate new tokens?
  - Will you need to setup anything else before hand to ensure only certain callers are allowed to generate tokens?
  - How are you going to store active tokens?
  - Will each token have a time limit on how long it will last before a new one has to be generated?   

### Reporting

Expand your application with a new API that will allow accounts to generate the latest report of their account activities.

Example Request:
```
POST http://localhost:8443/report
{
  "account_id": 1,
  "start_date": "1/1/2025",
  "end_date": "1/2/2025"
}
```

Example Response:
```
HTTP Code: OK 200
{
  "message": "Account ID 1 report generation complete."
  "timeline": [
    {
      "date": "5/1/2025"
      "name": "Tesco shopping",
      "amount": 20.00
    },
    {
      "date": "6/1/2025"
      "name": "Domino's Pizza",
      "amount": 35.00
    },
    {
      "date": "10/1/2025"
      "name": "CRUD BANK INTEREST",
      "amount": 5.00
    },
    {
      "date": "10/1/2025"
      "name": "ACCOUNT SETTLEMENT",
      "amount": 50.00
    }
  ]
  "report": {
    "total_purchases": 55.00,
    "total_interest": 5.00
    "total_settlements": 50.00,
    "latest_debt": 10.00
  }
}
```

- How will you have to alter your overall application in order to have ability to report on account data?
- Are there any other useful metrics you can pull out as part of the account reporting?
- Could you find a way to report on all accounts and find totals from the perspective of the bank?
  - e.g. total amount of all debt, interest earned and so on.
