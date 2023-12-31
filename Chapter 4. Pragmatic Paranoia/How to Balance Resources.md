## Intro
* When it comes to resources the general flow is the following:
	* allocate -> use -> deallocate
* Some people do allocate & use but forget the last part!
* Best tip is to **finish what you start**
	* If you allocate a resource in a function/object, just deallocate it in that function/object
* Example of a bad habit:
```
/*
	In the following example, we open a file in read_customer but close it in write_customer

	First of all, @customer_file is shared in two functions. So changing the implementation in read_customer also requires changes in write_customer
*/

def read_customer
	@customer_file = File.open(@name + ".rec", "r+")
	@balance = BigDecimal(@customer_file.gets)
end

def write_customer
	@customer_file.rewind
	@customer_file.puts(@balance.to_s)
	@customer_file.close
end

def update_customer(transaction_amount)
	read_customer
	@balance = @balance.add(transaction_amount,2)
	write_customer
end
```
* Suppose we make a slight change to update_customer as follows:
```
/*
	In this instance, we have an edge case where we can open a file in read_customer and not close it when the if condition isn't triggered.

	Obviously, we need to rework the way we close a file. Instead of closing it in write_customer, we could try to close it here as well. But then we should share @customer_file in THREE functions.

*/
def update_customer(transaction_amount)
	read_customer
	if (transaction_amount >= 0.00) {
		@balance = @balance.add(transaction_amount,2) 
		write_customer
	}
end
```
* Best fix: 
```
/*
	We've eliminated the instance variable for the shared file and now have a parameter that is passed in. 

	The only function that is responsible for the original file is update_customer.

	Likewise, that function also handles closing the file.
*/

def read_customer(file)
	@balance = BigDecimal(file.gets)
end

def write_customer(file)
	file.rewind
	file.puts @balance.to_s
end

def update_customer(transaction_amount)
	file = File.open(@name + ".rec", "r+")
	read_customer(file)
	@balance = @balance.add(transaction_amount,2)
	file.close
end

/*
	Even better is by restricting
	the scope of the file into this block. This handles closing the file
	for us.
*/
def update_customer_2(transaction_amount)
	File.open(@name + ".rec", "r+") do |file|
		read_customer(file)
		@balance = @balance.add(transaction_amount,2)
		write_customer(file)
	end
end
```

## Nest Allocations
* Say we need to allocate more than one resource..
* We should:
	* deallocate resources in the opposite order in which we allocate them
	* if we allocate the same set of resources in different places in our code, we should allocate them in the same order
		* this reduces **deadlock**
## Objects and Exceptions
* If we are using OOP and we find ourselves needing to use the same resource over and over again:
	* encapsulate the resource in a class
	* Make an object of that resource type
## Balancing and Exceptions
* If an exception is thrown, how do we ensure everything that might've been allocated prior to this exception is cleaned up correctly?
	* Options are:
		* Use variable scope
			* In Rust, if we open a file, when the variable associated with this is out of scope it is cleaned up
			* We can also pass in a destructor
		* Use a finally clause
## An Exception Antipattern
* Problems with using finally option:
```
/*
	If allocate fails, we go to
	finally which will deallocate something that never existed
*/
begin
	thing = allocate()
	process(thing)
finally
	deallocate(thing)
end
```
* 
```
/*
	This is better since we
	only enter the finally if
	allocation occured.
*/
thing = allocate_resource()
begin
	process(thing)
finally
	deallocate(thing)
end
```
## When You Can't Balance Resources
* If you have a dynamic data structure that has lots of substructures, it may be hard to deallocate
* You need to establish a semantic invariant
* Key idea: delegate who is responsible for data in a large data structure
* Three possibilities:
	* top-level structure is responsible for freeing any substructures
	* top-level structure is deallocated and substructures are orphaned (not a fan of this...)
	* top-level structure cannot be deallocated if there are substructures intact
* Author's suggestion:
	* Write a module for each major structure and provide allocation/deallocation procedures so this routine is consistent throughout codebase
## Checking the Balance
* Write wrappers for each resource that will keep track of allocations and deallocations
* Use those wrappers to see the state of the resources throughout program flow
* Suppose there is a point in your code where we wait for a request:
	* here we can check resource usage during the wait
* Or just use tools that handle checking for memory leaks