# expense-tracker
Personal Expense Tracker API
This is a RESTful API for managing personal financial records. Users can record their income and expenses, retrieve past transactions, and get summaries by category or time period.

Installation and Setup
Pre-requisites:
Install Node.js: Download
Install MongoDB: MongoDB Atlas
Steps:
Clone the repository:

bash
Copy code
git clone https://github.com/username/expense-tracker-api.git
cd expense-tracker-api
Install Dependencies:

bash
Copy code
npm install
Set up MongoDB:

Use MongoDB Atlas for a cloud database, or install MongoDB locally.
Create a .env file in the root directory and configure the following:

makefile
Copy code
MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/expenseDB
PORT=5000
Run the server:

bash
Copy code
npm start
Server will run on http://localhost:5000.

API Endpoints
Transactions
1. Add Transaction
URL: /api/transactions
Method: POST
Body:
json
Copy code
{
  "type": "income or expense",
  "category": "category_name",
  "amount": 100,
  "description": "Optional description"
}
Response:
json
Copy code
{
  "_id": "unique_transaction_id",
  "type": "income",
  "category": "Salary",
  "amount": 1000,
  "description": "Monthly salary",
  "date": "2023-10-22T14:28:06.875Z"
}
2. Get All Transactions
URL: /api/transactions
Method: GET
Response:
json
Copy code
[
  {
    "_id": "unique_transaction_id",
    "type": "expense",
    "category": "Food",
    "amount": 50,
    "description": "Dinner",
    "date": "2023-10-22T14:28:06.875Z"
  },
  {
    "_id": "unique_transaction_id",
    "type": "income",
    "category": "Salary",
    "amount": 1000,
    "description": "Monthly salary",
    "date": "2023-10-22T14:28:06.875Z"
  }
]
3. Get Transaction by ID
URL: /api/transactions/:id
Method: GET
Response:
json
Copy code
{
  "_id": "unique_transaction_id",
  "type": "income",
  "category": "Salary",
  "amount": 1000,
  "description": "Monthly salary",
  "date": "2023-10-22T14:28:06.875Z"
}
4. Update Transaction
URL: /api/transactions/:id
Method: PUT
Body (fields you want to update):
json
Copy code
{
  "amount": 1200
}
Response:
json
Copy code
{
  "_id": "unique_transaction_id",
  "type": "income",
  "category": "Salary",
  "amount": 1200,
  "description": "Monthly salary",
  "date": "2023-10-22T14:28:06.875Z"
}
5. Delete Transaction
URL: /api/transactions/:id
Method: DELETE
Response:
json
Copy code
{ "message": "Transaction deleted successfully" }
Summary
1. Get Summary
URL: /api/summary
Method: GET
Response:
json
Copy code
{
  "income": 2000,
  "expense": 500,
  "balance": 1500
}
Error Handling
The API returns appropriate HTTP status codes and messages in case of errors:

400 Bad Request: Invalid data or missing required fields.
404 Not Found: Transaction not found.
500 Internal Server Error: Server-side issues.
Example error response:

json
Copy code
{
  "message": "Transaction not found"
}
Summary Endpoint
The /api/summary endpoint returns the total income, total expenses, and balance. It aggregates the transaction data stored in MongoDB.

You can extend this by adding filters like date ranges or specific categories to provide more detailed insights.

Example Usage (Postman)
Add Transaction:

Open Postman, create a POST request to http://localhost:5000/api/transactions.
Add the following body:
json
Copy code
{
  "type": "income",
  "category": "Salary",
  "amount": 1000,
  "description": "Monthly salary"
}
Get Transactions:

Create a GET request to http://localhost:5000/api/transactions.
Get Summary:

Create a GET request to http://localhost:5000/api/summary.
