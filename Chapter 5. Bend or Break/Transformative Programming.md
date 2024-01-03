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
* 