# Embed Python/DevOps assignment

## What to build

For this assignment, you will build a backend web service that enables users to publish posts and subscribe to other user's posts. Pretend like Embed devs should be able to integrate with your backend web service and run it inside our infrastructure. You'll also have to prepare some auxiliary services that will make state of the backend service (especially errors and bad performance) more observable.

## What do you need

To complete this assignment you will require the following:

* Python >= 3.8
* any Python web framework e.g. Flask, Bottle, CherryPy, Tornado, Django, FastAPI (it's recommended to pick the one you feel most comfortable with)
* any data store for storing the data models and user data e.g. PostgreSQL, MariaDB, MongoDB, Cassandra, CouchDB, Riak, Redis, Memcached (it's recommended to pick the one you feel most comfortable with)
* private GitHub or Bitbucket account and public git repository where you will upload the code
* use RESTful or GraphQL or gRPC (the choice is yours) to implement the APIs
* Docker engine >= 17.0 (for docker-compose specification >= 3.2)

## Functional requirements

### User registration

* User is able to register by selecting a username and password
* User may not register if the username is already taken
* User may not register if the password is not strong enough (define some rules e.g. minimum 10 characters, a mix of letters, numbers and special characters)
* After registration is complete, user should receive an authorization token to use

### User login

* User can't log in if the username and password are not correct
* After the login is complete, the user should receive an authorization token to use

### User posts

* User can publish a post at any time, post must have a title (e.g. up to 100 characters long) and post text can be only up to 1000 characters long
* User can search his/her posts by the title name via a simple substring match (e.g. searching "sport" should return any post titles such as "The best sporting events in town", "Scream SPORT if you like it", "Sport in everyday life")
* Output of the search should be a list of tuples: post title, post text

### Managing user subscriptions

* User can view all the other usernames available and how many subscribers they currently have
* User can subscribe to any other user simply by adding their username to the list of subscriptions
* User can't subscribe to a username that doesn't exist
* User can remove a subscription at any time
* User can have up to 100 subscriptions, no more than that

### Filtering user subscriptions

* User can search through his/her subscriptions by using any of the following filters: list of usernames, simple substring match for the post title, simple substring match for the post text
* List of usernames should have a limit (e.g. up to 10 usernames) and should contain usernames that exist
* Output of the search should be a list of tuples: username, post title, post text

### Logging events

* Every time a user interacts with the backend service (using any of the APIs) we want to be able to track it by leaving a trace of that interaction (e.g. simply using logging module in Python or something more advanced)
* We also want to be able to track if any user interaction has resulted in an error and try to get as much details as possible about the error and the request that caused the error
* Add an auxiliary service capable of scraping those log/trace events and making them available for searching/filtering using a dedicated interface or API
* Don't build this auxiliary service by yourself, use some of the existing open-source tools that will do the job for you
* Filtering log events doesn't have to contain advanced rules, simple substring matching will do (e.g. search if the log event contains "error")

### System usage monitoring

* We want to be able to track system usage of existing Docker container that is running the backend web service
* Tracking metrics like: CPU usage/load, memory usage/load, storage usage, inbound/outbound network etc.
* System metrics should be collected and then visualized using some of the existing open-source tools fit for this job
* Visualization of system metrics doesn't have to be too detailed, showing numbers and percentages would do as well

## Non-functional requirements

### Backend service

* Access to user posts and subscriptions should be protected via an authorization token
* Response time should be limited to 2 seconds for every non-search request
* Response time should be limited to 30 seconds for every search request
* In case of an error, the response should provide some kind of feedback about the error (e.g. 404 Bad Request with response body "Username does not exist")
* Should be able to sustain up to 100 daily active users
* Should be able to sustain up to 10 parallel active users
* Add a sufficient amount of documentation in the code according to what you feel necessary in case anyone else would take over this project from you in the future

### Data store

* All the user data should be persisted on local storage, which means when the backend service is restarted (e.g. after a crash) no user data is lost
* Access to the data store from the backend service should be as secure as possible
* All created data structures should be optimized to maximize the speed of required queries (triggered by the backend service)
* Should be able to sustain up to 1000 unique user profiles
* Should be able to sustain up to 100 parallel connections

### Auxiliary services

* Log events and system metrics should be both persisted if possible with retention of at least 24 hours
* Scraping frequency for log events should be approximately 10 seconds or less
* Collecting frequency for system metrics should be approximately 30 seconds or less

## Docker development environment

Docker development environment should be reproducible on another host so that your code can be run and tested by Embed devs.

Make sure that each dedicated service runs in its own Docker container and provide information on how to use auxiliary services that you added.

Note: This is also possible to solve using Kubernetes (e.g. using `minicube`) and that approach could reflect production environment more realistically. It's probably easier to use `docker-compose` instead just for the purpose of this assignment, but we will not discard solutions that use local Kubernetes cluster or some other approach (anything you find more appropriate to use to solve this assignment).

## The output of an assignment

When you finish with the assignment, please prepare the following:

* Code and other resources uploaded on your private GitHub or Bitbucket account
* Share the link to your public git repository (from GitHub or Bitbucket) where you uploaded everything so the Embed dev team can check it out
* `README.md` file with instructions on how to build, configure and run your code (the service and the data store) and how to use the auxiliary services to observe log events and system metrics
* `DOCS.md` file (or multiple files) where you documented all of your APIs so the Embed dev team can see how to integrate (or if you're using something to auto-generate the docs like OpenAPI/Swagger that will do as well)

## Final note

The intellectual property of this code is only yours, feel free to leave it on your GitHub or Bitbucket account as open source if you like and use it as a showcase for future purposes. Embed will not request the removal of the code once the assignment is complete and verified.

If you have any additional questions or require assistance, please don't hesitate to contact us via e-mail: [iva@embed.xyz](iva@embed.xyz)
