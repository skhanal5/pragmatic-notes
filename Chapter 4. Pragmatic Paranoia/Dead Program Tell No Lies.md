## Catch and Release Is for Fish
* ```
```
/*
	The following is a BAD example.
	We are getting errors from the function we invoke
	and catching them, and then producing a new error...
*/
try do
	add_score_to_board(score);
rescue InvalidScore
	Logger.error("Can't add invalid score. Exiting")
rescue BoardServerDown
	Logger.error("Can't add score: board is down. Exiting")
	raise
rescue StaleTransaction
	Logger.error("Can't add score: stale transaction. Exiting")
	raise
end
```
* 
```
/*
	A much better example
	- There is no coupling here. Suppose, add_score_to_board
	  changes it's contract and has new errors later on
	- Errors are propogated back directly
*/
add_score_to_board(score)
```
## Crash, Don't Trash
* TLDR: let program crash when it supposed to crash
* There are two main approaches on handling programs that have crashed or are supposed to crash
	* Have a supervisor that handles the crash case
		* i.e., cleans code, restarts it, etc.
		* supervisors are a tree-like structure: one supervisor looks over the other supervisor (in case it crashes)
	* clean up resources, write logs, tidy transactions, etc. before exiting
* 