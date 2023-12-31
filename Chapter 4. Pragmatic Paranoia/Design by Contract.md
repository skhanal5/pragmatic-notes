## DBC
* Design by contract is a technique that documents the rights and responsibilities of software modules to ensure correctness
* Correctness
	* Does exactly what it claims to do
	* Verified and documented in the contract
* Expectations
	* Preconditions
		* the requirements for the routine to be called
		* Should not be called if these conditions are violated
		* Caller passes in good data, callee doesn't have to handle that
	* Postconditions
		* What the routine is guaranteed to do
		* State of the world when the routine is finished
		* Aside: ensures the routine will 'complete'
	* Class invariants
		* A rule that will always be true in the perspective of the caller
		* When control flow is given back to the caller, the invariant must hold
			* Technically, DURING the invocation it doesn't have to, as long as it does when it returns
	* What happens if all terms cannot be held by either party?
		* Exception
		* Program termination
	* Before you begin implementing a function, be clear on the inputs you will accept so that you will not have to do further validation in the body of the function
## Assertions
* Take this a step further by having the compiler check the contract for you
* Assertions allow you to do this
	* They are limited though, you cannot send assertions down inheritance hierarchy in OOP languages
	* Exceptions might be turned off or ignored in the code
	* Runtime systems/libraries are not designed to support this
## Dynamic Contracts and Agents
* Not all contracts are fixed
* There can be cases where an agent can reject requests or renegotiate contract