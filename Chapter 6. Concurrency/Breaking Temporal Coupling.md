## Intro
* Two important aspects of time to consider:
	* concurrency
	* ordering
* When we design systems it is usually in a linear manner:
	* For example: do this and then do that
## Look For Concurrency
* Figure out the flow of the application
* Determine what can happen at the same time and what must happen in a specific order
* Draw an activity diagram
	* Draw all actions
	* Arrows from one action go to another action or to a line called a synchronization bar
	* If all actions going to a synchronization bar are finished, you can proceed along any arrows leaving it
	* An actions w/ not arrows leading in to it can be started at any time
* From there, figure out what can be performed in parallel
## Opportunities for Concurrency
* Find activities that take time and then determine if you can run something else in the meantime
	* Querying a database, waiting for user input, etc.
## Opportunities for Parallelism
* Find pieces of work that are independent
	* Take a large piece of work
	* Split it into independent chunks
	* Process each in parallel
	* Combine the results