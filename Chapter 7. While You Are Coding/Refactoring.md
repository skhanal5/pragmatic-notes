## Intro
* Think of software engineering as gardening rather than construction
* Rewriting, reworking, and rearchitecting code = restructuring
* A subset of this is called refactoring
	* Changing the internal structure of code without changing its external behavior
* Refactoring should occur daily
	* Low-risk small steps
	* Targeted approach -> don't just decide to change the entire codebase one day
	* To ensure you haven't changed the behavior of the code, you need good automated unit testing
## When Should You Refactor?
* When to refactoring:
	* Duplication
		* [[DRY - The Evils of Duplication]]
	* Nonorthogonal design
		* [[Orthogonality]]
	* Outdated knowledge
		* Some requirements change
	* Usage
		* Realize that some features are more important than others
	* Performance
		* Need to move functionality from one area to another
	* Tests Pass
		* When you write something and your tests pass, go back and refactor it real quick
### Real-World Complications
* People use time pressure as an excuse to not refactor
* If you wait even longer to refactor, it will be a greater time investment later on
* Refactoring is easier when the issues are small
	* If you need a full rewrite let others know
## How Do You Refactor?
*  Tips:
	* don't refactor and add functionality at the same time
	* have good tests before refactoring and run them often
	* take short, deliberate steps
		* move a field from one class to another
		* split methods
		* rename variables
	