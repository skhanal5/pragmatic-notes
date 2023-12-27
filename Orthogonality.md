## What is Orthogonality?
Two or more components are orthogonal if changing one doesn't affect the other

## Benefits of Orthogonality

Increased Productivity
- Changes are localized
- No need to change existing code as you add new code
Reduce Risk
- Bad code is isolated
- System is less fragile
- Easier to test
- Not tied to one vendor/platform
## Design
Layered approach
- Each layer only uses the abstractions provided by the layers below it
- So if you design a system, changing one layer should only affect that one layer
* Don't rely on properties of things you have no control over (i.e., phone numbers)

## Toolkits and Libraries
Measure how introducing a toolkit may impose any changes on your codebase (i.e., adding more objects)

## Coding
Keep your code decoupled
- Write code that doesn't depend on other module's implementations
- Write code that doesn't expose extra information either 
- Avoid global data
- Avoid similar functions
## Testing
* Can test individual modules 
* When fixing bugs, if you find yourself needing to change multiple things -> refactor

## Living with Orthogonality
DRY vs Orthogonality
* DRY -> minimize duplication
* Orthogonality -> reduce interdependency among system's components (think decoupling)