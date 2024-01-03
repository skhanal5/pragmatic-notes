## Events
* We want to write applications that respond to events and adjust to what they do based on those events
* There are four strategies discussed below that will help us write these types of applications
## Finite State Machines
* Consists of a set of states, one of them is the current state
* For each state, we write the events significant for that state
* For each of those events, define a new current state of the system
* We can represent FSM's as data (like a table)
	* Rows are states
	* Columns are events
	* Contents are new state
### Adding Actions
* We can add actions that are triggered on certain transitions
## The Observer Pattern
* We have a source of events called the *observable* and a list of clients called the *observers* who are interested in those events
* Observer registers with the observable (by passing a reference to a function that should be called)
	* When the event happens, observable iterates over list of observers and invokes the functions
	* Event is a parameter to that call
* This introduces coupling
* Also is done synchronously -> has a bottleneck
## Publish/Subscribe
* We have *publishers* and *subscribers* which are connected through channels
* Channels are implemented in a separate piece of code -> abstracted away from us
* Subscribers register to channels and publishers write events to channels
* Communication between publisher and subscriber is handled outside of our code and can be *asynchronous*
* Cloud service providers have implemented this as well as languages
* Good because:
	* decouples handling of async events
	* Lets you add/replace code when app is running without modifying existing code
* Bad because:
	* hard to see what is going on inside
## Reactive Programming, Streams, and Events
* Say you have multiple values where one value depends on another. 
* Reactive programming is similar to the idea of where one value changing means another will also reactively change as well
* Vue.js / React.js are examples
* Streams treat events like collections of data
	* Think: arraylist of events
	* Can do array operations (filter, add, remove, etc.)
* Streams can be async too
### Streams of Events Are Asynchronous Collections
* Event streams combine synchronous and asynchronous processing in one API
* i dont understand this much
* 