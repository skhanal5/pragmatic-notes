## The Other 90%
* Analyze code for ways it can go wrong and add them to your test suite
	* bad parameters
	* memory leaks
	* etc.
* Always consider how external actors can break your system
* This is really alluding to cybersecurity
## Security Through Basic Principles
* Principles to always keep in mind:
	* Minimize Attack Surface Area
	* Principle of Least Privilege
	* Secure Defaults
	* Encrypt Sensitive Data
	* Maintain Security Data
* Shoutout CMSC414
### Minimize Attack Surface Area
* Defn: all places an attacker can use to enter data, extract data, or invoke execution of a service
* Places to look for:
	* Anywhere where your code is incredibly complex
	* Any places where you accept input data from the outside world
		* Sanitize input data -> view OWASP guides!
		* Some languages do this themselves
			* Ruby allows you to taint external data, ex: can't execute stuff from input data
	* Any places where users can call unauthenticated services
		* Do not put data in publicly readable data stores
		* I am guilty of this kinda
	* Authenticated services are an attack vector
		* Get rid of old users
		* Get rid of outdated services
		* Be wary of default passwords and unused/unprotected admin accounts
		* Deployment credentials!!
	* Output layer
		* Don't leak out information either
		* For example: messages like "password is used by another user" (lol)
		* Anything you report to the outside world should be appropriate for the sake of your company as well as its users
		* truncate/hide/blur secure information like social security numbers
	* Debugging Info
		* Make sure console.log statements don't leak out important information
		* Stack traces should be hidden to the outside world
		* [[Test to Code]] -> remember those test windows, hide that
### Principle of Least Privilege
* Idea is give the least amount of privilege for the shortest time to accomplish whatever is necessary
* Don't just hand out root/admin level perms
### Secure Defaults
* Make sure default settings is the most secure values
* Let the user's decide about trade-offs in regard to security when customizing things
* Example: by default we hide password input text
### Encrypt Sensitive Data
* Sensitive information should not be in plain text
	* This includes files or even worse a database
* In [[Version Control]] , we discussed repo's
	* Hide those secrets, API keys, SSH keys, encryption passwords, etc.
	* Also guilty of this
### Maintain Security Updates
* Download those patches
* Fix your code if it breaks after updating a dependency
## Common Sense vs Crypto
* First rule of cryptography: **NEVER DO IT YOURSELF**
	* use those libraries that are reputable (bcrypt)
* If you need a login with password authentication, they suggest using a third-party authentication provider