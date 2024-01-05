## Nonatomic Updates
* Use this example to understand:
	* We have two waiters, two customers, and one piece of pie
	* Both customers (dining separately) request this piece of pie, both waiters notice it is available and try to retrieve it
	* One waiter will get to the pie sooner, the other waiter will notice it is gone
	* A customer is unhappy
* If we represented this as code, we would first check to see the pie count, then promise to get the pie, take the pie, and give the pie to the customer
* The problem is neither program can guarantee it has a consistent view on this pie data
	* When one person retrieves the pie count and copies it over to their own memory -> it can become outdated
* Neither fetching and updating the pie count is atomic
### Semaphores and Other Forms of Mutual Exclusion
* Semaphores limit access so only one person can have ownership of a thing at one time
* Using the pie example
```
case_semaphore.lock()

if display_case.pie_count > 0
	promise_pie_to_customer()
	display_case.take_pie()
	give_pie_to_customer()
end
```
* So in the two waiter case, only one waiter will get the semaphore, the other will be blocked
* Problems:
	* Only works if everyone who accesses the underlying object (the pie count) agrees to use a semaphore
### Make the Resource Transactional
* The above approach basically tells the people who use this pie object to handle protecting it
* New approach
```
/* 
	we will check the count and 
	take a slice in one step
*/
slice = display_case.get_pie_if_available()
if slice
	give_pie_to_customer()
end

def get_pie_if_available()
	if @slices.size > 0
		update_sales_data(:pie)
		return @slices.shift
	else
		false
	end
end
```
* There is a problem, our method still has the race condition
```
def get_pie_if_available()
	@case_semaphore.lock()
	if @slices.size > 0
		update_sales_data(:pie)
		return @slices.shift
	else
		false
	end
	@case_semaphore.unlock()
end
```
* What if update_sales_data raises an exception...
	* Our semaphore will never be unlocked
```
def get_pie_if_available()
	@case_semaphore.lock()
	try{
		if @slices.size > 0
			update_sales_data(:pie)
			return @slices.shift
		else
			false
		end
	} finally {
		@case_semaphore.unlock()
	}
end
```
* Alternatively something like this in your language of choice:
```
def get_pie_if_available()
	@case_semaphore.protect() {
		if @slices.size > 0
			update_sales_data(:pie)
			return @slices.shift
		else
			false
		end
	}
end
```
## Multiple Resource Transactions
* Recalling the example above, suppose there is a 2-in-1 dish where the waiter needs to look for pie and ice cream
* Naturally, I'd come up with something like this:
```
slice = display_case.get_pie_if_available()
scoop = freezer.get_ice_cream_if_available()
if slice && scoop
	give_order_to_customer()
end
```
* Problem:
	* Suppose we get a slice of pie but there is no ice cream
	* Remember, our code does both checking and retrieving at once (if amount is > 0)
* I'd end up coming with some nasty check like this:
```
slice = display_case.get_pie_if_available()

if slice
	try {
		scoop = freezer.get_ice_cream_if_available()
		if scoope 
			try {
			give_order_to_customer()
			} rescue {
				freezer.give_back(scoop)
			}
		end
	} rescue {
		display_case.give_back(slice)
	}
```
* I hate code that turns out like this
	* So many edge cases
* Before:
	* we fixed by moving resource handling code inside of the resource itself
	* Now, we can't do this because we have two resources (would have to pick one or the other)
* Suggested solution:
	* Make a new resource that represents the combined dish and put it in there
	* Infeasible: can have multiple combined dishes
* Define some type of menu item which has references to its components
	* Have a generic get_menu_item method that handles the resources
## Non-transactional Updates
* Concurrency problems can be whenever there are multiple instances of code trying to access a shared resource
	* Doesn't need to be in-memory; think databases and files
* Tip: random failures are probably concurrency issues
## Other Kinds of Exclusive Access
* Mutexes, monitors, or semaphores are all ways of having exclusive access
* Some languages like Rust have data ownership where one variable can hold a reference to one piece of mutable data at a time
## Doctor, It Hurts...
* Concurrency is hard, look at the next two sections for easier ways of handling this stuff