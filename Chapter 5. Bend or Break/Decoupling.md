## Intro
* Decoupled code is easy to change
* Suppose A is tied to B and B is tied to C and D, a change in A invokes a change in B,C, and D
## Train Wrecks
* See the following sample code:
```
public void applyDiscount(customer, order_id, discount) {

totals = customer.orders.find(order_id).getTotals();
totals.grandTotal = totals.grandTotal - discount;
totals.discount = discount;

}
```

* Lots of implicit knowledge here:
	* You need to know customer object can find orders
	* Orders have a find method
	* You can get a totals objects and update it
* Say you need to add a max discount limit. Where do you add this change?
	* Totals can be modified by anyone, so this change needs to be added in different places
* Totals should be handling updating the totals yet anyone can query and update it
* To fix this, apply the **tell, don't ask** approach
	* Don't look at the state of an object and then update it
* To fix the above example:
```
public void applyDiscount(customer, order_id, discount) {

	customer
		.orders
		.find(order_id)
		.getTotals()
		.applyDiscount(discount);
}
```
* Now, the totals object handles applying the discount rather than us modifying it
* We should apply the same logic to the customers where we find the order we want directly rather than going through all the orders
```
public void applyDiscount(customer, order_id, discount) {

	customer
		.findOrders(order_id)
		.getTotals()
		.applyDiscount(discount);
}
```
* Take things up a notch and encapsulate the getTotals part"
```
public void applyDiscount(customer, order_id, discount) {

	customer
		.findOrders(order_id)
		.applyDiscount(discount);
}
```
## The Law of Demeter
* A method defined in a class C should only call
	* Other instance methods in C
	* Its parameters
	* Methods in objects that it creates, both on the stack and in the heap
	* Global variables
* The above law is a little strict and not practical for all scenarios
* **New suggestion:** Try to limit the number of method calls you make
	* Don't want a long chain of them
	* Don't have a sequence where you create an object, then invoke a method, and then use the results to invoke another method, and so on either
## The Evils of Globalization
* Global data are a huge source of coupling
* Think of it as an additional parameter that can be passed in every method that of that module
* Refactoring requires you to find all instances
* This includes Singletons and external resources (API's, DBs, etc)
	* Wrap this behind code you control
* If its important to be global, wrap it in an API