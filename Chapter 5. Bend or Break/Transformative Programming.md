## Intro
* Stop thinking of classes, modules, frameworks, etc.
* Think of programs as things that transform inputs to outputs
## Finding Transformations
* Start with the requirement and determine its inputs and outputs
* Find steps that lead you from input to output
* Example: build a website with a word game that lets users find all words from a set of letters
	* Take input
	* Get all combinations of three or more letters
	* Get a *signature* of these words (basically sort the word by letter so words, anagram situation)
	* Find dictionary words that match that signature 
	* Group words by length
### Transformations All the Way Down
* Think of step two -> getting combinations
* You can break this down into its own transformation (think generating unique combinations)
* Textbook uses Elixir example with |> operator
	* This kinda of shows you how data goes from one transformation to another
## Why Is This So Great?
* Our code just becomes a chain of transformations that is easy to understand
* This is better than OOP approach where each part of the chain is its own class and we attempt to change each other's instance variables
* Chain of functions better here
## What About Error Handling?
* Basic convention: **never pass in raw values between transformations**
	* Wrap them in a type or a data structure instead
* When writing code: Handle checking for errors inside transformation or outside it
### First, Choose a Representation
* Use a representation for the wrapper
	* Looks something like this:
		* (ok, value)
		* (error, reason)
### Then Handle It Inside Each Transformation
* The idea here is if we encounter an error, it should propagate down the chain
* One way of handling this is:
	* for each function in the chain, have a duplicate function that takes in the error "wrapper" as a argument in place of a value
	* When that error function runs, it will return the error forward
#### Or Handle It in the Pipeline
* Think of Elixir's pipeline operator, now imagine it had a way of knowing about the error/value wrappers and can short circuit execution s.t. when we get an error