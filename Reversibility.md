## Introduction
* Don't expect to be using one specific pattern, vendor, etc.
* Critical changes are often not reversible yet you have to deal with change as it comes anyways
## Reversibility
* Ideally, abstract out any services (or anything really) so that *if* changes come, you can easily implement those changes
* Sometimes, changes come from within rather than externally 
## Flexible Architecture
* Hide third party API behind your own abstraction layers
* Break code into components
* You'd rather have it split up from the get go rather than splitting it up later
