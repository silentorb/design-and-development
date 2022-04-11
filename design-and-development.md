# The Design and Development of Elegant Systems

## Cost Visibility

### Background

* Every tool has a cost
* Junior developers are attracted to tools that make grand promises and hide the expense
* Senior developers are more likely to value tools that are up-front about their cost
* If a tool appears to have many obvious weaknesses that have well defined boundaries, there is less likely to be major surprises beyond those weaknesses

### Rules

* If a tool appears to have few weaknesses, know that it probably has signicant weaknesses that are hard to determine
* If the authors of a tool seem oblivious to the cost and weaknesses of the tool, be wary of that tool

## Dependencies are Expensive

### Background

* Dependencies are essential
* Dependencies are expensive
* Dependencies add requirements to any system that depends on them
* At minimum, dependencies add the requirement that they must be available
  * A component will not function as well or at all without its dependencies
* Dependencies may add constraints to their dependents
  * For example, 
* Some dependencies are incompatible with each other and force mutually exclusive selection

* Different dependencies have different costs
  * One heavy dependency can potentially cost more than a dozen light dependencies.

### Rules

* Weigh the cost of dependencies
* Minimize dependencies, especially heavy dependencies
  * But don't [reinvent the wheel](don't-repeat-yourself)

## Don't Repeat Yourself

### Rules

* Minimize duplicate code within a codebase
  * Especially for business logic
    * If a pivotal calculation is performed in a system, there should be one authoritative function for that equation
* When reusing common code across multiple codebases, put that code in a library



## Flat over Nested

> Flat is better than nested - The Zen of Python

### Rules

* Prefer flat logic over nested logic when organizing objects of the same level of specificity
  * In other words, minimize nesting except to nest general solutions within specific solutions
* When a problem requires nested logic, a nested solution can sometimes still employ flat data structures
  * For example, a DAG can be represented as a flat collection of references

## Invisible Walls

> "I taught you everything you know. But I didn't teach you everything I know." - Orson Scott Card, Ender's Game

### Background

* All problems have a finite number of practical solutions and an infinite number of impractical solutions
* Most endeavors follow conventional paths
  * To one degree or another, conventional paths are practical solutions
* Innovation is the act of finding new, viable solutions
* Most unexplored solutions are dead-ends
* Innovation requires trial and error
* Successes are documented more than failures
* Through trial and error, when a person arrives at a viable solution, that person will understand why not to attempt the seemingly viable neighboring solutions and will not repeat those mistakes
* A person who uses a successful solution without experiencing the trial and error will not be aware of the surrounding pitfalls and is more likely to repeat the mistakes of that solution's inventors
  * It is usually much cheaper to make those mistakes when prototyping than it is with an established product

### Rules

* When innovating, know that the world is full of invisible walls
  * Walls that are neither obvious nor common knowledge and have been slammed into by others
* When entering a new problem domain, know that established competitors are probably aware of invisible walls you are not aware of
* Value trial and error and the deeper understanding they provide
* Be wary of inventors who accidentally arrive at a solution without first stumbling against invisible walls
  * Those inventors will invariably run into invisible walls later and make the mistakes *after* people are depending on their solutions
  * This is related to [knowing the cost](cost-visibility)

## Mortal Growth

> The best code is the code designed to die

### Background

* In the world of biology, organisms grow by replacing old cells with new cells
* Humanity grows by standing on the shoulders of its predecessors
* Any major improvements upon a system require the removal of previous components
* The more experimental a system, the more it requires temporal stepping-stone components
* Sometimes too much effort is put into short-lived components 
* When a system is monolithic, replacing components can easily break other components throughout the system
* A system can efficiently handle experimentation and growth when it is designed to have most or all of its components replaced

### Rules

* When designing a system, anticipate that system being replaced someday
* Divide a system into smaller parts that can be replaced without breaking other parts of the system

## Specialization

### Rules

* Each tool should do one thing and do it well

## Temporal Narcissism

> "Those who fail to learn from history are condemned to repeat it" - Winston Churchill

### Background

* Everyone stands on the shoulders of their predecessors
* Every tool you use and every tool you create is [mortal](#mortal-growth)
* The greatest impact of a design is not the design itself, but its influence on later designs

### Rules

* Study what others have designed in the past
  * Find cases of what succeeded *and* what failed
* Create designs that are not only useful to you now, but to others in the future
  * This is design legacy

## The Doctor's Dilemma

### Background

* When there is damage inside a person's body, all health practitioners face the same challenge: the damaged area is surrounded by one or more layers that prevent direct interaction with the damaged area
* How does one get at the damaged area?
  * Some options are:
    * Trigger chemical reactions
    * Apply surface forces
    * Cut them open

* Systems need to be divided into layers
* Even if a system is not divided into layers, it is probably built on top of other layers and other layers may be built on top of it

* Layers are useful because they compartmentalize, but they can also create problems because they obscure

### Rules

* Don't create tools that get in the way
* Minimize the layers of a system, preferring [flat over nested](#flat-over-nested)
* Make the contents of your layers as accessible as possible
* Design with maintenance in mind, which often involves features that are only used for maintenance

