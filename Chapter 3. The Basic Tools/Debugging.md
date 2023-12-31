## Psychology of Debugging
* Debugging is problem solving
* Don't start blaming people or making excuses, if you find a bug -> resolve it
## A Debugging Mindset
* Don't panic
* Critically think of reasons that can trigger a particular bug
* Don't brush a bug off as impossible
* Discover the root cause of the problem and fix it -> don't just do the bare minimum fix
## Where to Start
* First ensure the code built cleanly (no warnings)
	* Set compiler warning to max level
* Gather all relevant data
	* May include watching someone produce the bug or reproducing it yourself
	* Brutally test boundary conditions and realistic end-user patterns
## Debugging Strategies
* Reproduce the bug
	* Don't reproduce the bug by following a sequence of steps
	* Try to reproduce it with a single command
	* Isolate the circumstances that display the bug
		* Write tests and fail those tests
* Read any error messages
* If we have a bad result
	* Naturally, use the debugger
	* Ensure you see the wrong value in the debugger
	* Pen & paper strategy also helps
* If bug is produced by particular input data
	* use binary chop to isolate which values after getting a copy of the original input and running it locally
* If a bug is produced in a new release
	* binary chop those releases
* Note: binary chop = binary search
* If bug is related to the state of a program over time (temporal situation)
	* stack trace doesn't help
	* use print statements here
* Explaining to a partner
	* Might be able to expose problem through conversation
* Don't go blaming other things in use: OS, third party libraries, etc.
	* Chances are it is you
	* Even if it is that *other* thing, you need to be able to determine it isn't your code at fault
* Don't gloss over things that have been consistent or things that you are comfortable with
	* Surprises happen
	* In case this thing does break, figure out why it didn't break sooner and amend it
		* Tests
		* Parameter checking
		* Log file analyzers
		* Team understanding