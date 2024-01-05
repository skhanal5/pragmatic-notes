## Intro
* Concurrency: execution of two or more pieces of code *act* as if they run at the same time
	* Code can switch execution between different parts of your code
	* Think: fibers, threads, processes
* Parallelism: when two pieces of code *do* run at the same time
	* Hardware that can make use of multiple cores
	* or multiple computers
## Everything is Concurrent
* Lots of things are happening around the same time in the real world
	* Users interacting
	* Data fetched
	* Services invoked
* Serial processes are slow
* *Temporal Coupling* is a problem where your code imposes sequence on things that is not inherently required to solve a problem
	* For example: accessing multiple services one by one in a sequence
* Biggest problem is shared state
	* Any instance where two chunks of code have references to the same piece of multable data