# API Sample Test

## Getting Started

This project requires a newer version of Node. Don't forget to install the NPM packages afterwards.

You should change the name of the ```.env.example``` file to ```.env```.

Run ```node app.js``` to get things started. Hopefully the project should start without any errors.

## Explanations

The actual task will be explained separately.

This is a very simple project that pulls data from HubSpot's CRM API. It pulls and processes company and contact data from HubSpot but does not insert it into the database.

In HubSpot, contacts can be part of companies. HubSpot calls this relationship an association. That is, a contact has an association with a company. We make a separate call when processing contacts to fetch this association data.

The Domain model is a record signifying a HockeyStack customer. You shouldn't worry about the actual implementation of it. The only important property is the ```hubspot```object in ```integrations```. This is how we know which HubSpot instance to connect to.

The implementation of the server and the ```server.js``` is not important for this project.

Every data source in this project was created for test purposes. If any request takes more than 5 seconds to execute, there is something wrong with the implementation.

## Response to the Assignment

I implemented the functionality to fetch and process meetings from HubSpot, extracting properties like the meeting 
title and timestamps. For contacts attending meetings, we used the crm.associations API to fetch associated contact IDs
and retrieved their emails through crm.contacts. Actions for “Meeting Created” and “Meeting Updated” were generated, 
ensuring all meetings are processed regardless of whether associated contacts were found.

I have seen and noticed that the actions drained from the queue are not written back to the mongodb, left it as-is since
there were no instructions about it on the notions doc, sorry if I missed that.

For meetings without associated contacts, I chose to skip them to reduce unnecessary processing and 
storage of incomplete data. However, other approaches could include allowing for potential reconciliation 
in the future while maintaining timely processing. Alternatives I considered included adding a placeholder value like 'unknown' or 'missing';
or retrying API calls to see if they'd yield them.

As the assignment asks, please find my improvement items below:

Improvements

	1.	Code Quality and Readability:
	-	Break large functions into smaller, single-purpose methods for better clarity.
	-	Improve naming consistency and add inline comments where necessary.
	2.	Project Architecture:
	-	Introduce a service layer to isolate API interactions from business logic.
	-	Implement a logging and monitoring system to handle errors and retries transparently.
	3.	Code Performance:
	-	Implement caching mechanisms for frequently accessed data like contact emails.
	-	Optimize processing by parallelizing independent tasks, such as fetching emails for multiple meetings.
    4. Testing:
    -   Add unit and integration tests to ensure quality and correctness