## Intro
* Actor: an independent virtual process with its own local state
	* It has a *mailbox*
	* When the mailbox is empty, it is sleep
	* When the mailbox is nonempty, the actor wakes up and processes the message in it
		* During this time, it can:
		* create other actors
		* send messages to other actors
		* create a new state that will be the current state when the next message is processed
* Process: a general-purpose virtual processor -> handled by the OS (think: 216)
	* constrained by convention to behave like actors
## Actors Can Only Be Concurrent
* There is no single thing in control (spontaneous)
* Only state is held in messages + local state of each actor
	* Cannot access local state outside of the actor
	* Cannot read messages 
* Messages are one way
	* You can return a response by providing your mailbox
* Processes each message to completion and only one message is processed at a time
* This reminds me of SQS
* TDLR: Async, concurrent, shares nothing
## A Simple Actor
* Using Pie example to mimic message flow:
	* Someone (not important) tells the customer they are hungry
	* Customer tells waiter
	* Waiter asks the pie case (from before)
	* If pie case is nonempty, send pie to customer and notify waiter to update bill
	* If pie is empty, notify waiter to tell customer
* Customers can receive three messages:
	* You're hungry (meaning we want pie)
	* There is pie on the table (we got pie from pie case)
	* There is no pie (waiter sent this)
```
	const customerActor = {
	'hungry for pie': (msg, ctx, state) => {
			return dispatch(state.waiter, {
				type:"order",
				customer:ctx.self,
				wants: "pie"
			})
		}
	}
	'put on table': (msg,ctx,_state) => 
		console.log(`${ctx.self.name} sees "${msg.food}" appear on the table`)
	'noe pie left': (msg,ctx,_state) => 
		console.log(`${ctx.self.name} is sad`)
```
* This is the waiter's actor:
```
const waiterActor = {  
"order": (msg, ctx, state) => {
	if (msg.wants == "pie") {
		dispatch(state.pieCase,
		{ type: "get slice", customer: msg.customer, waiter: ctx.self }) 
	else {
		console.dir(`Don't know how to order ${msg.wants}`)
	}
},
"add to order": (msg, ctx) =>
	console.log(`Waiter adds ${msg.food} to ${msg.customer.name}'s order`),
"error": (msg, ctx) => {
	dispatch(msg.customer, { type: 'no pie left', msg:msg.name});
	console.log(`\nThe waiter apologizes to ${msg.customer.name}: ${msg.msg}`)
	}
}
```
* Now imagine a similar structure for the pie actor
* Actors are started dynamically by other actors usually
* The following is a manual invocation of the actors:
	* Some state includes:
		* Pie case gets a list of slices it has
		* Waiter has a reference to the pie case
		* Customer has a reference to the waiter
```
const actorSystem = start()

let pieCase = start_actor (
	actorSystem,
	'pie-case',
	pieCaseActor,
	{
		slices:[insert types of slices]
	}
)

let waiter = start_actor(
	actorSystem,
	'waiter',
	waiterActor,
	{pieCase: pieCase}
)

let c1 = start_actor(
	actorSystem, 
	'customer1', 
	customerActor, 
	{waiter:waiter}
)

let c2 = start_actor(
	actorSystem, 
	'customer1', 
	customerActor, 
	{waiter:waiter}
)

//dispatching 
dispatch(c1, { type: 'hungry for pie', waiter: waiter });
dispatch(c2, { type: 'hungry for pie', waiter: waiter });
```

## No Explicit Concurrency
* Actor model doesn't handle concurrency because there is no shared state
* idk if I fully understand this but it kind of makes sense
## Erlang Sets the Stage
* Erlang has processes, not the OS version, but lightweight and you can run millions at a time
* There is no sharing of state like Actors
* Also has a supervision system
	* Can restart processes if they fail
* Hot-code loading
	* Can replace code in a running system without stopping