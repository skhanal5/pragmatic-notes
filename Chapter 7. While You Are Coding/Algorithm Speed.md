## What Do We Mean By Estimating Algorithms?
* Nontrivial algo's have variable input
	* Size of input affects the algo's speed (runtime & spacetime)
* If you write anything containing loops or recursive calls
	* Be sure to have your runtime and memory requirements in the back of your head
## Big-O Notation
* Throwback/review
* Usually denote the worst-case time taken of the algorithm
	* The upper-bound
* Just keep track of our highest order term when approximating
* Used for runtime & spacetime (don't forget the memory)
## Common Sense Estimation
* Some of them are trivial
* Loops -> O(n)
* Nested loops -> O(n^2)
* Binary chop -> O(logn)
* Divide and conquer -> O(nlogn)
* Combinatoric -> O(n!)
## Algorithm Speed in Practice
* More than likely won't have to worry about writing our own algo's
* Should always be asking yourself about how large your input values are
	* Bounded -> can determine precisely the speeds
	* Unbounded -> think deeper
* If you are unsure, test with varying input sizes
	* Use *practical* tests, random number generators may not be a good way of testing all cases
### The Best Isn't Always Best
* Quicksort often recognized as the best sorting algorithm but Insertion Sort is more practical for smaller input sizes
* Also think about the overhead of setting up some of these algorithms
* Be wary of premature optimization where we try to improve an algorithm before determining where the performance bottlenecks are