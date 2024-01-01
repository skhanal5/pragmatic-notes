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