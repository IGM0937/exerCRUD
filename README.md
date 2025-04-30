# exerCRUD

Small repository containing a small exercise specifications for creating a new CRUD REST API project.

## Overview

The example specificaiton looks to create a CRUD REST API project for a example credit card provider, CRUD_bank.

The following specification is used for new comers to the world of Software Engineering 🌍 🖥️

### Recommended prerequisites 

Before starting the project, think about some baseline questions:

- What language are you looking to use?
- What database are you going to utilise?
  - Will it be relational? NoSQL?
- What utility will you use to send API requests and see the responses?
  - Will it be another service applicaiton all together?

Here are some baseline recommendations:

- Selecte a good IDE
  - VSCode is popular and versitile at the time of writting.
  - JetBrains line of community products (the ones that are free).
  - If you want to be a 10x giga-chad developer, use Neovim or Emacs (not recommended for beginners). 
- Use Docker containers to easly setup your database instance.
  - Do look into data persistancy. There are some docker containers that will remove your data once you turn off the containers.
  - Recommend looking into relational databases like SQLite and Postgres.
- Utilise existing and trusted open source libraries for:
  - Any HTTP server creation for your API endpoints.
  - Any connections to a database of your choice.
- For API utilities, you can use Postman, Insomnia, Hoppscotch, Milkman or even some plugins that come built into IDE

Majority of recommendation will require some research just any of the above information is out of date.

## Base Specification

The following section will provide the very basics of the project to get you started.

### Accounts

#### Create User

The ability to create a user who has joined CRUD_bank.

Example Request:
```
POST http://localhost:8443/user/create
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
GET http://localhost:8443/user/1
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
PUT http://localhost:8443/user/1
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
DELETE http://localhost:8443/user/1
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
  - Do you just use one table or do you seperate the inforamtion out to seperate tables and why?
- How do you generate a new account ID?
  - Do you use the primary key of a database?
  - Do you randomly generate a number when the user is created?
- What are the available HTTP code responses available in a typical REST API?
- For each endpoint, are there any validation you want to do on the incoming payloads?
  - e.g. Are all the expected fields available? If not, mabye send back an appropriate error response?
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
  "purchase_name": "Tesco shopping",
  "purchase_cost": "20.00"
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

- How will you represent the users accound balance in the database?
- Will an account have a spending limit?
  - e.g. If so, what type of error resopnses do you want to show?
- Can the response message be expanded with useful information?
  - e.g. Could you inform the user of their latest credit card allowance and limits?

### Settlements

The ability for a user to settle their credit card debt.

Example Request:
```
POST http://localhost:8443/settle
{
  "account_id": 1,
  "settlement": "20.00"
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
  - (in the real word, credit card companies don't like people overpaying their debt, because they can't charge interest on those accounts!)

## Extra CRUD_bank features

### API Authentication

### Interest

### Reporting
