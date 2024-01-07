## Intro
* Authors say testing isn't about finding bugs
## Thinking About Tests
* First write out the signature of the method you are writing
* Then think about the tests for this method, assuming this method is done
	* What would you pass in?
	* How would you pass it in?
	* What information do you need (fields in a db, etc.)?
* Update your signature with this new information
## Tests Drive Coding
* Thinking about tests reduce coupling and increase flexibility (see previous example)
	* When we need to test a function that is coupled, we need to setup an environment
	* If we make our function readily testable, chances are it is decoupled
* We also perceive the code we right in terms of the client
	* A test is the first user of your code
* Always understand the function before you even try to test it
	* If you write the function on a whim, then it'll probably end up being a lot longer than necessary
	* Ex: figuring out error and boundary conditions along the way, resulting in large conditionals
	* If we think about the boundary and error conditions prior to coding, we might find patterns and make our code cleaner
### Test-Driven Development
* TLDR: Write the test before writing the code
* Cycle is:
	* decide on a small piece of functionality to add
	* write a test that will pass when the functionality is added
	* run all tests (verify the only failure is the one you wrote)
	* write the smallest amount of code needed to get tests to pass
	* refactor the test and/or the code
* Problems:
	* people seeking 100% test coverage
	* lots of redundant tests
	* designs start bottom up
## TDD: You Need To Know Where You're Going
* Another problem is that TDD can steer you on a path where you focus on easy problems and ignore the bulk of the problem you are solving
	* you will be sidetracked by small things and constantly refining
## Back to the Code
* We want to build testability into the software from the get-go and test each piece thoroughly before trying to tie things together
* Think in components
## Unit Testing
* Code that exercises a module
* Usually in unit testing, we do the following:
	* make an envrionemnt
	* invoke routines in the module we care about
	* check returned results against known values or previous values (latter is regression testing)
* Gives us confidence our individual units work
## Testing Against Contract
* Unit testing should be testing against the given things contract
	* [[Design by Contract]]
* We want to ensure that that thing holds up on its word
* Example: a square root function
	* Its contract is :
		* that the argument must be >= 0
		* difference between the square of the result and the original argument is less than some small fraction of the argument
			* basically our square root should be less than the argument itself 
* From here we can test the following:
	* square root of 0
	* square root of a negative value
	* square root of a known value (64)
	* square root of a large value
* How do we unit test a module that is dependent on other modules?
* Example: module A uses a DataFeed module and a LinearRegression module:
	* they say test DataFeed's contract
	* test LinearRegression's contract
	* A's contract
* Helps in debugging:
	* if DataFeed and LinearRegression pass but A fails, A is the problem
## Ad Hoc Testing
* Poking at our code manually
	* Using console.log
	* A REPL
	* IDE
	* Debugger
* After doing an ad-hoc test, formalize it using a unit test
## Build a Test Window
* Tests will not spot all the bugs possible
* You will need to test software once it is been deployed using real world data
* We can see what is going on internally using logs after deployment
	* Log files can have trace messages
	* Ensure the format of log messages are consistent and regular
	* Or use a secret menu (via hidden link or hot key sequence)
## A Culture of Testing
* Three approaches
	* Test first
		* best choice
	* Test during
		* write some code, play with it, write tests for it, move onto the next portion
	* Test never
		* obviously bad
* Keep test code clean, decoupled, and robust
	* [[Programming by Coincidence]]
		* Don't make this mistake
	* 