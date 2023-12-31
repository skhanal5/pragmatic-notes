## Intro
* Prototyping is inexpensive compared to full-scale production
* Software prototypes are good to find risk, offer chances for correction at reduced cost
	* Post-it notes for workflow
	* Wireframes for UI
* Can be poorly made as well (ignoring important requirements/details)
* Determine if Tracer Bullets is better if your in a situation where you cannot give up crucial details
## Things to Prototype
* Anything with risk, anything new, anything your doubtful about
	* Architecture
	* Third party tools
	* UI
	* Contents of external data
## How to Use Prototypes
What details can we ignore?
* We have four main categories:
	* Correctness
		* Dummy data
	* Completeness
		* Work w/ 1 type of input 
		* Work w/ one menu item
	* Robustness
		* Have incorrect error checking or it is missing
	* Style
		* Minimal/no documentation or comments
* Consider using high level languages
* For UI use Figma
## Prototyping Architecture
* None of the individual modules need to be particularly functional
* Focus Areas
	* Are responsibilities of major areas well defined and appropriate
	* Are collaborations between major components well defined?
	* Is coupling minimized?
	* Can you identify potential sources of duplication?
	* Are interface definitions and constraints acceptable?
	* Does every module have an access path to the data it needs during execution? Does it have that access when it needs it?
## How Not to Use Prototypes
Ensure the prototype isn't actually deployed