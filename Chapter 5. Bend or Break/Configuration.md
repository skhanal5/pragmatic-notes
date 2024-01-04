## Intro
* If you code relies on some values that can change after the app goes live (keys, passwords, etc.), keep those things external to the application
* Parameterize your application by keeping environment/customer specific values outside the app
* Things like:
	* credentials
	* log levels
	* ports and ip addresses
	* cluster names
	* environment params
	* externally set params (i.e., tax rates)
	* site-specific formatting stuff
	* license keys
## Static Configuration
* Configuration is usually in flat files or database tables
* For flat files 
	* Use Plaintext ([[The Power of Plain Text]])
	* Use YAML or JSON
* If the information is structured and can be changed by a client
	* Use a database
* When we use these values in the app itself, it will usually be in a data structure with global visibility 
	* Wrap it behind an API instead
## Configuration as a Service
* Service API for configuration stuff
* Benefits are:
	* multiple apps can share this API
	* API can offer varying levels of authentication/control
	* Config data can be maintained with a specialized UI
	* Config data is dynamic
		* No more need to start and stop a service to update values