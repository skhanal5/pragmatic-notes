## Intro
* Recurring theme is we find ourselves in situations convincing ourselves that X,Y, or Z cannot possibly happen and yet it can
* Handle this by using assertions
* Recall: assertions check for things that **can never happen.**  assertions **DO NOT** replace error handling
* Also, you are not required to let the assert terminate when it fails -> can be a good place to free resources
## Assertions and Side Effects
* Be careful with triggering some type of side effect when using assertions
```
while (iter.hasMoreElements()) {
	// with this assertion, we move our iterator once
	assert(iter.nextElement() != null);

	// and then we move it one more...
	Object obj = iter.nextElement();
}
```

```
while (iter.hasMoreElements()) {
	// here is the intended effect
	Object obj = iter.nextElement();
	assert(obj != null);
}
```
* Simple but tricky mistake
## Leave Assertions Turned On
* Do not take off assertions when you ship your code
* A poor assumption is thinking it is not needed at deployment because they only look for things that never happen
* There is no chance we can test for all possible bugs 
* If this is a performance related concern
	* Can turn off those that hit the most