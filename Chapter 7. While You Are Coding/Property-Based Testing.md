## Contracts, Invariants, and Properties
* Recall: [[Property-Based Testing]]
* Alongside the contracts we guarantee for a function, there are *invariants* that are things that hold true about input passed into a function
	* For example: a sorted list should have the same # of elements before and after invoking the sort function
* This is a property
* Another property is that no element in the resulting list can be greater than the element that follows it
* Property based testing allows us to test these properties using variable inputs in aggregate
## Test Data Generation
* Property based libraries give you a mini-language to define the data it should generate
	* This is better than using RNG because sometimes RNG isn't an accurate representation of real-world data
	* We can hone down our RNG to be more similar to practical situations
* Example:
```
from hypothesis import given
import hypothesis.strategies as some

@given(some.integers(min_value=5, max_value=10).map(lambda x: x*2))
```
## Finding Bad Assumptions
* Real world example:
	* Order processing and stock control system
	* Models stock levels with a Warehouse object
		* Query to see if something is in stock
		* Remove things from stock
		* Get current stock levels
	* For testing purposes, suppose we make an order function that allows us to order an item of specified quantity from the warehouse
		* returns (status, item, quantity)
```
class Warehouse:
	def __init__(self, stock):
		self.stock = stock
	def in_stock(self, item_name):
		return (item_name in self.stock) and (self.stock[item_name] > 0)
	def take_from_stock(self, item_name, quantity):
		if quantity <= self.stock[item_name]:
			self.stock[item_name] -= quantity
		else:
			raise Exception("Oversold{}".format(item_name))
	def stock_count(self, item_name):
		return self.stock[item_name]


//proptest/stock.py
def order(warehouse, item, quantity):
	if warehouse.in_stock(item):
		warehouse.take_from_stock(item, quantity)
		return("ok", item, quantity)
	else:
		return("not available", item, quantity)
```

* Property based test:
	* One idea is that after ordering, the amount we order + the amount remaining = initial amount
	* Problem:
		* in_stock doesn't check to see if the quantity we order is valid
## Property-Based Tests Often Surprise You
* Frustration arrives from PBT's because the bug may not be clear that causes the test to fail
* Suggestion:
	* find out what parameters are passed into test function
	* Use those values to make another unit test
	* You can focus on the problem in an isolated environment without additional calls
		* regression test pretty much
	* Remember: PBT's generate many random values so you may not get the value that caused your test to fail next time
## Property-Based Tests Also Help Your Design
* [[Test to Code]] -> helps you think about the way your approaching your code
* PBT's -> helps you think about the code in terms of invariants & contracts
	* Removes edge cases
	* Highlights functions that leave data in inconsistent state
