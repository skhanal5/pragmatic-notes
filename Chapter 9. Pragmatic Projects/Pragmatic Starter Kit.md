## Drive With Version Control
* [[Version Control]]
* Everything becomes ephemeral with version control
* Deployment config can be under version control allow on automatic releases
* We want build, test, and deployment to be triggered through commits & pushes, and built in a container
* Release to staging and production is specified by a tag
## Ruthless and Continuous Testing
* Use unit tests to spot small errors and bugs
* Use integration tests to find the big problems
* Test early, test often, and test automatically
* Automatic build runs all tests
	* test environment should match production environment closely
### Unit Testing
* unit test tests a module
	* [[Test to Code]]
* make sure your modules work before you proceed doing the stuff listed below
### Integration Testing
* Subsystems should work together cohesively
* Integration is usually the largest source of bugs
* Make sure each subsystem honors their contracts
### Validation and Verification
* When you make a UI or prototype, ask yourself if what you made is what the user really needs
* does it address the requirements
* be aware of how users use/access things not
### Performance Testing
* Does your software meet the performance requirements under real-world conditions?
* Is it scalable?
### Testing the Tests
* When you write a test to find a bug, cause the bug again and make sure the test actually works
* You can even go crazy and introduce a bunch of bugs in a separate branch and see how it works
* Netflix's Chaos Monkey is something interesting to read
### Testing Thoroughly
* You can't ever have assurance that you've testing enough
* code coverage is a common metric but it doesn't paint the full picture
* To get to the full picture, you'd have to think about all possible states of your program and try to test each possibility
	* pretty hard lmfao
### Property-Based Testing
* Have a computer generate those states mentioned above
* Find your invariants and test them
* [[Property-Based Testing]]
## Tightening the Net
* If you find a bug, add a test that checks to see if that bug is now caught
* Automated tests should always be modified and up to date with new bug funds
## Full Automation
* We rely on scripted, automated procedures
* (Aside: i need to learn how to do this stuff)
* Avoid manual procedures
* Even if dev's have slightly differing environments, we know that shell scripts will run the thing we specify it to