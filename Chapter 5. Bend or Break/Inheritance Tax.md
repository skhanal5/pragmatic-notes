## Problems Using Inheritance to Share Code
* Inheritance obviously brings coupling
* Think of things like super class methods, super class instance variables, and so on
### Problems Using Inheritance to Build Types
* People use inheritance to define new types
	* Then people defined layers on top of other layers to differentiate those types
* Multiple inheritance is another issue
	*  For example: a Car can be a Vehicle, Asset, InsuredItem, etc.
## The Alternatives are Better
* Three techniques to replace inheritance:
	* Interfaces and protocols
	* Delegations
	* Mixins and traits
### Interfaces and Protocols
* Define interface contracts to lay out the methods your class should have implemented
	* Think Java
* Interfaces are powerful because we can use them as types
* Ex: Locatable interface with Car and Phone classes that implement this interface
	* We can create a list of Locatable's and it can have both Cars and Phone's
	* More importantly, we know it is safe to use the interface methods irrespective of the underlying Class type
### Delegation
* Inheritance is also dangerous because we can have a super class with say 30 methods and a subclass that only needs 2 of those methods
	* it will still have access to the remaining 28 
* If we used delegation instead, we don't expose the framework API and aren't limited by it either
	* We can have our own API too
	* Technically in inheritance, you can have your own API as well but there is a risk it will be bypassed by superclass
### Mixins, Traits, and More
* Mixins: extend class and objects without using inheritance
	* Make a set of functions and extend an object to include it
* Example: AccountRecord wraps an Account
	* Account uses Persistence framework 
	* We don't want all of the Persistence API to be exposed to the outside world
	* We can write a Mixin that implements some standard functions we want to expose
	* For other classes that use Persistence, we can apply this same Mixin
	* If you need code that does some type of validation, you can bundle it in its own mixin and then apply it