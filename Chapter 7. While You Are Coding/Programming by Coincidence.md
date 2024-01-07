## Intro
* Don't strive to be lucky, program deliberately
## How to Program By Coincidence
* Most of the time people don't know why their code is failing is because they literally don't know why it worked in the first place (lmao sounds like me)
	* Limited testing further boosts false confidence
### Accidents of Implementation
* Accidents happen because:
	* the way the code is written relies on boundary conditions
	* For example: you invoke a routine with bad data and the routine responds in a particular way
	* So you write your entire code relying on this type of response
	* If you end up finding out the routine was incorrect and you fix it, chances are your code is broken now
* Now suppose your code does work, even when its not supposed to
* For example: your code invokes a bunch of routines in a sequence, but it isn't supposed to be called like this
	* Don't leave it alone (another warning to me)
	* There is a good chance, it simply doesn't work
	* If it works under your local conditions, it may not work in other environments
	* May not work in future releases of dependent libraries
	* You are probably slowing down your code with those method calls
		* Each method call adds more bugs
* Always document your assumptions!
### Close Enough Isn't
* Think about situations where your code is *only off* by some numeric value (let's say 1)
* If this is the case, don't be lazy and leave it as is and try to account for this error by throwing in a +/-1 (or some way of counteracting the error)
* Think about the following:
	* Developers realize this error and for each subsequent function that depends on your code, they add a +/- 1
	* Some other function may be off by 1 the other direction and revert the previous changes
* Your code has a **fundamental error**, go back and fix it
### Phantom Patterns
* Sometimes we see patterns in coincidences
* For example, suppose we have a log files that sees an error every X amount of requests
	* We may think this is a race condition, or a simple bug
* Or we have tests that pass locally but not in the server
* Is it coincidence or not?
	* literally figure it out
### Accidents of Context
* We may make assumptions (that aren't always true) like
	* assuming English users when making a GUI
	* assuming we have access to environment/config files when we need them
	* assuming some type of network speed/bandwidth
	* assuming code we copied from the Internet works for our situation... lol
### Implicit Assumptions
* Testing is a big place where assumptions and coincidences occur simultaneously
* By assuming X we see it causes Y
* Document assumptions!!!
## How to Program Deliberately
* Tips:
	* Be aware of what your doing
	* Ensure you can explain every line of code you wrote
	* Don't build something OR work with something you don't fully understand
	* Have a plan
	* Rely on reliable things (No assumptions)
	* Document assumptions
	* Test assumptions too
	* Spend time on important aspects (the hard parts)
	* Don't restrain yourself to the existing codebase