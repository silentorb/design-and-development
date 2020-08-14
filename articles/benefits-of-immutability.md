
## Benefits of Immutability

### Removes a certain class of side-effects

Immutable data structures remove the possibility that a block of code can change a value another block of code is in the middle of processing.  While this is most prominent in concurrent code, this can also happen in sequential code, where a block of code can invoke another block of code that unexpectedly modifies a variable the first block is using.

Immutability does not remove all side effects.  Software systems still involve dependencies, and changing a dependency will still result in a different, dependency-related class of side-effect.

### Raises the immediate visibility of complexity and its cost

Complexity comes with a price tag.  Part of the attraction of mutating data is it hides complexity and defers its cost.  In some cases, the cost can be deferred indefinitely, never needing to be paid.  In other cases, the cost catches up with the project and requires payment, usually with interest.

At first glance, an immutable solution often looks more complicated than an equivalent mutable solution.  That is because the inherent complexity of the problem being solved is more accurately communicated in the immutable solution.  This reduces future problems, eases predictable planning, and gives developers a better understanding of the current problem domain.

### Synchronizes changing state with logic

Both mutable and immutable systems contain state that changes over time.  In a mutable system, the data is the state that is changed over time via logic.  In an immutable system, the data is constant, merely samples along a graph, while the logic itself is the state changing over time.

This gives immutable logic a clearer role.  It is purely data flow.  It transitions from one state to another.  Mutable logic has the dual roles of data flow and modifying data.  (It is possible to create logic that purely modifies state without any data flow but that is usually impractical.)

This also allows immutable code to better communicate how time factors into its structure.

### Consolidates state changes

In a mutable system, meaningful changes to state can be easily be applied anywhere.  In an immutable system, applying meaningful changes to state is harder, because state changes must be folded into the larger data flow to have any effect.

This forces the developer to consolidate when certain parts of state are changed.  For example, a game loop where a player's health is represented as a numerical value that can be changed over time by a variety of different causes.  In a mutable game structure, it is easy and common for there to be different lines of code all over the codebase where the player's health is modified.  In an immutable game structure such an approach is painful to create and generally impractical.  With an immutable system it is easier to have a single place in the game loop where the player's health is modified (via a new game state).  What value the player's health is changed to can be determined by a collection of factors that are gathered and funneled into that final line of code that changes that players health.

The end result is code that is easier to reason about and debug, and contains less surprises.  If a bug arises where the player's health is an unexpected value, the developer can start at the single point in the game loop where that value is modified, and work backwards.

Such funneling can also be implemented in a mutable system, but mutable code does not encourage or enforce that direction.

### Function signatures become more expressive

When a function can directly mutate global state, return values are non-essential and optional.  When a function is immutable, the only impact it has on the larger app is through its return value.  The entire effect of an immutable function is restricted to its return type.  If a function returns a new User object and User objects do not contain any references to Company objects, there is no way that function can have any direct impact on Company objects.

In mutable code the parameters of a function are more significant than the return type, while in immutable code the return type is more significant than the parameters.  When writing mutable code, it is normal to think first in terms of the parameters to a function, and then figure out what the function should return (if anything).  When writing immutable code, it is normal to think first about what the function should return, and then figure out what parameters will be needed to derive the desired result.

This is in part why some functional programming languages have lazy resolution: functional programming lends itself well to a pull-driven workflow.

