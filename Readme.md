This project was build to calculate the reward points based on transactions : 

A retailer offers a rewards program to its customers awarding points based on each recorded purchase as follows:
 
For every dollar spent over $50 on the transaction, the customer receives one point.
In addition, for every dollar spent over $100, the customer receives another point.
Ex: for a $120 purchase, the customer receives
(120 - 50) x 1 + (120 - 100) x 1 = 90 points

Environment details : 
Language : Java 8
Framework : Spring boot
Database : H2 
Documentation tool : Swagger 

Health check endpoint : curl http://localhost:8080/actuator/health
Swagger end point : http://localhost:8080/swagger-ui.html#

Rest end points : 
	URL : http://localhost:8080/rewards/{startDate}/{endDate}?startDate=2022-05-20&endDate=2022-05-24
	HTTP Method : Get
	Description : Use this end point to fetch the reward points per customer between the given dates.
	Sample response : 
	[
	  {
		"id": 1,
		"month": "MAY",
		"points": 353
	  },
	  {
		"id": 2,
		"month": "MAY",
		"points": 707
	  }
	]
	
	URL : http://localhost:8080/transactionList
	HTTP Method : POST
	Description : Use tihs end point save list of transactions.
	Sample input : 
		[
		  {
		"customerId":1,
			"amountSpent": 100,
			"transactionDate": "2022-05-20"
		  },
		  {
		"customerId":1,
			"amountSpent": 200,
			"transactionDate": "2022-05-21"
		  },
		  {
		"customerId":2,
			"amountSpent": 150,
			"transactionDate": "2022-05-22"
		  },
		  {
		"customerId":2,
			"amountSpent": 300,
			"transactionDate": "2022-05-23"
		  }
		]
	Sample output : 
		[
		  {
			"id": 1,
			"customerId": 1,
			"transactionDate": "2022-05-20",
			"amountSpent": 100
		  },
		  {
			"id": 2,
			"customerId": 1,
			"transactionDate": "2022-05-21",
			"amountSpent": 200
		  },
		  {
			"id": 3,
			"customerId": 2,
			"transactionDate": "2022-05-22",
			"amountSpent": 150
		  },
		  {
			"id": 4,
			"customerId": 2,
			"transactionDate": "2022-05-23",
			"amountSpent": 300
		  }
		]
	
	URL : http://localhost:8080/transaction
	HTTP Method : POST
	Description : Use tihs end point save one transaction at a time.
	Sample input : 
	  {
		"customerId":1,
		"amountSpent": 100,
		"transactionDate": "2022-05-20"
	  }
	Sample output : 
	  {
		"id": 1,
		"customerId": 1,
		"transactionDate": "2022-05-20",
		"amountSpent": 100
	  }