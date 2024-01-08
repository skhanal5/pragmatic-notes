## Intro
* When naming things name them according to the role they play in the code itself
* "What is my motivation for creating this" 
	* "Why does this thing do what it does"
* Example: let user = authenticate(credentials)
	* Service allows people to access site to sell jewelry
	* user could be "customer" or "buyer" instead
* Example: public void deductPercent(double amount)
	* Method allows us to discount an order
	* deductPercent tells us what the method does and not the why
	* amount can be misleading, we don't know the format of this value
	* Suggested change: public void applyDiscount(Percentage discount)
* Example: a module called Fib that contains a method that generates the nth Fibonacci number
	* Named fib -> standard practice
	* Problem is the method is now invoked Fib.fib(n)
	* Suggested change: rename method to of or nth (Fib.of(n) or Fib.nth(n))
## Honor the Culture
* People say don't use i,j,k -> but it depends on the context of the. language we use
* camelCase vs snake_case
## Consistency
* Ensure everyone in the team understands the jargon that is being passed around
* Have a project glossary
## Renaming is Even Harder
* Rename misleading names as you find them
	* Leaving it as is can make code very hard to understand
	* Essence of [[Software Entropy]], if you don't fix it then the problem propagates further
* If you cant change it, we have an ETC violation as discussed in [[The Essence of Good Design]]
* 