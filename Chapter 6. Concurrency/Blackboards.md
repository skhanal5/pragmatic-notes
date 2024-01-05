## Intro
* Scenario: think of an investigation of a crime scene where there is a blackboard with initial findings that ends up growing to include new evidence, possible suspects, etc.
* Main ideas of the blackboard approach:
	* Though many people can contribute to the board, the identity of those people is irrelevant
		* Status/background of those people is also irrelevant
	* People may contribute at different times
	* We care about the new findings on the blackboard as well as being able to add our own contributions
	* No restrictions on what can be on the blackboard
* The ways blackboard works in code is:
	* Store object or data on the blackboard and then use pattern matching/partial matching to query it
## A Blackboard in Action
* Example: want to write a program to handle mortgage & loan apps
* Problems to consider:
	* Responses can come at any time (i.e., credit checks)
	* Data gathering can be done from many different people at different times & places
		* Time to process may be different as well
		* Async possibly
	* Some pieces of data may rely on other places of data (i.e., need proof of ownership to search a car's title)
	* Arrival of new data may raise questions
* Instead of making a large workflow to address all combos, use a blackboard with a rules engine
	* For each fact that is posted, we can determine if it triggers our rules (in case the federal/state laws)
	* Output of any rules will also be posted on the blackboard and trigger more rules
## Messaging Systems Can Be Like Blackboards
* Kafka, SQS/SNS, NATS, etc. offer persistence (see event logs), ability to retrieve messages through pattern matching
	* Also Actor functionality
## But It's Not That Simple
* Every "alternative" approach we discussed is a lot harder to reason about
* Need a good way of tracing messages and facts
	* Suggested to use trace id's
* Keep a central repository of message forms and API's
* Hard to deploy and manage
