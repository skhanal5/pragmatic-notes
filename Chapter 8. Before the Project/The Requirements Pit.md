## Intro
* People usually say the first part of a project is to gather the requirements
* But most of the times, we don't know the requirements or they aren't clearly defined
## The Requirements Myth
* In the real world, the exact specifications are rare or unknown
* Our job is to help people understand what exactly it is they want
## Programming as Therapy
* Clients may come to use with a need
* Needs aren't immediate requirements
	* Always go a step further an *ask questions* (something you don't do at all)
	* Remember the client probably *knows* the answer to these questions but is assuming that whatever you produce magically has these questions in mind
	* Sometimes you need to be diplomatic and suggest policy issues
* Example: client wants a feature where shipping is free on all orders $50 or more
	* Questions include:
		* Does the $50 indclude tax?
		* Does the $50 include current shipping charges?
		* What kind of shipping is offered? Priority? Ground?
		* Will the $50 promo end?
	* Diplomatic issues:
		* $25 book with $25 overnight shipping -> shipping is free -> $25 total cost b/c of free shipping promo (client takes big losses)
## Requirements Are A Process
* Requirements are gathered in a feedback loop with your client
* If you don't have enough domain exp -> ask "is this what you meant" after showing a prototype
## Walk In Your Client's Shoes
* Change perspectives to get a feel for how your product will be used
## Requirements vs Policy
* Example: "only supervisors and personnel can view an employee's record"
	* Business requirement
	* Fixed today but may be lax another time
	* Implemented through checks at the moment someone tries to access data
* Rephrase as "Only authorized users may access an employee record"
	* Implemented via an access control (idm system)
* Policy is metadata -> design systems where this metadata can easily be altered
## Requirements vs Reality
* Remember your tools should be able to adapt to what the clients needs are
* "it does what I want but not how I want it"
## Documenting Requirements
* Requirements should be milestones (ex: design docs)
### Requirement Documents Are Not for Clients
* Don't produce large design docs based off of a brief conversation with your client
	* Client's don't read these things
### Requirement Documents Are For Planning
* Doc's are good for *developers*, so make one for your team so everyone knows what they are doing
	* Make it short and concise
	* Authors suggest it should fit in a index card
	* idea is to ask questions that further expand on this
* user stories: describe app functionality from the perspective of the user
## Overspecification
* Don't be too specific
* Abstract, should reflect the business need
## Just One More Wafer-Thin Mint
* Project failures are blamed b/c of increase in scope (too many features/requirements)
	* [[Stone Soup and Boiled Frogs]]
* Feedback prevents this -> client will pick and choose what features matter
## Maintain a Glossary
* Terms will have specific meanings in regard to requirements
* All members on the team should have access to it