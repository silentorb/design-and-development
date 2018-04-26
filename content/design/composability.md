# Composability

##  Separation of Concerns

Complexity is just a bunch of simple.  No matter how large and complex a problem is, it can be cleanly solved if it is divided into enough smaller pieces.

However, the divisions cannot be arbitrary. Like chopping wood or carving a turkey, proper division of a complex problem requires dividing along existing lines. In a way, such division is simply accentuating existing lines.

A commonly used method of division is known as Separation of Concerns (SOC).  What is a concern? Within the context of software development, the definition of "concern" is fuzzy. Sometimes it is used to refer to a particular purpose, role, or domain. Dividing a system along such lines can be useful, but can also lead to equally fuzzy boundaries.

When attempting to understand and apply the concept of Separation of Concerns, it is more useful to define concerns and their boundaries through dependencies. When two components of a system have radically different dependencies or radically different dependents, that lends weight to keeping those parts separate. When two components of a system share similar dependencies and dependents, that lends weight to packaging those parts together.

While organizing the components of a system in such a manner does not reduce the dependencies of that system, it does reduce the dependencies for each component of the system.  This is good because

## Dependencies are Expensive

Dependencies are a two-edged sword. On one hand, everything except God is dependent on something. Dependencies are essential.  But they are also expensive.

Dependencies add requirements to any component that depends on them. At minimum, dependencies add the requirement that they must be available. The component will not function as well or at all without its dependencies. Beyond that, dependencies can add additional requirements in the form of constraints. Constraints on how and where the component can be used. Some dependencies are incompatible with each other and force mutually exclusive selection.

Beyond the added constraints, dependencies can make a component harder to manage and reason about because each added dependency increases the complexity of that component.

Different dependencies have different costs.  In terms of weight, one heavy dependency can cost more than a dozen light dependencies.

##  Monoliths

Breaking separation of concerns leads to monoliths.  Monoliths are bad.

##  Hubs

Sometimes a system is designed in such a way that it is divided into many components with very clean separation of concern, and then all of those components are tied to a single "master" or "god" component.  Master components are like dieting during the weekdays and then Ice Cream binging over the weekend.

Master components usually have two problems:

    1. They have too many dependencies
    2. On top of connecting dependencies they add implementation logic.

The first problem can be solved by breaking up the Msater component into smaller pieces.  The second problem can be solved with the hub pattern.

A hub is a component with the following properties:

    1. It packages multiple dependencies.
    2. It contains little to no implementation logic.  It's simply a dumb package.
    3. It does not encapsulate it's dependencies.  (Though it could provide some additional shortcuts to aspects of its dependencies).

 The hub pattern divides components into two groups: hubs and implementation.  Either a component has many dependencies and little implementation logic or it has a lot of implementation logic and few dependencies.

##  Driving Dependencies

When a chain of dependencies is used to solve a particular problem, the dependencies along that chain are arranged from specific to general.

When a developer creates a game, a common structure is to create a project for the game, which in turn is built on top of a game engine, both of which are built using a programming language.

The game project is a particular solution; it is designed to create a single game. The game engine is a more general solution; it is designed to create a variety of games. The programming language is an even more general solution; it is designed to create a wide variety of software beyond just games.

Out of each of those three components, the game project contains the most details about the particular problem being solved. It is hardcoded to meet the specifications of the particular game. The game engine contains less details about the game, and the programming language contains even less.

Thus, the game project is the most well-suited out of the three components to direct how the other components operate. The game project should drive the game engine and both should drive the programming language.

In the same way, dependents should drive dependencies.  Dependents should be responsible for the lifetime and operation of their dependencies.

Here is a graph to help visualize this organization:

|  Game  | Engine | Language |
| :----: | :----: | :------: |
|   1    |   2    |    3     |

Where lower numbers are more specific solutions and higher numbers are more general solutions.  Notice how the numbers are ordered from lowest to highest.

##  Plugins

Instead of creating a particular component that manually includes and manages multiple dependencies, developers sometimes create a plugin manager to take the place of the particular component.

A plugin manager is a general component that manages a dynamic assortment of specific components.  it is a dependency that drives dependents.  It breaks the logical flow of a system's dependency chain.

To use the previous game example, a clean dependency structure is:

|  Game  | Engine | Language |
| :----: | :----: | :------: |
|   1    |   2    |    3     |

When the game engine is turned into a plugin system, it results in a graph like:
 
|  Game  | Engine | Plugins | Language |
| :----: | :----: | :-----: | :------: |
|   1    |   3    |    2    |    4     |

Notice how the numbers are no longer ordered.  The more general plugin engine gets in the middle of the more specific game project and plugins.

A cleaner and more flexible organization would be to use libraries instead of plugins and have these libraries controlled by the game project, not the game engine.  This would result in a graph like:

|  Game  |  Engine   | Language |
| :----: | :-------: | :------: |
|        | Libraries |          |
|   1    |   2       |    3     |

Now, both the engine and libraries are parallel dependencies of the game project.  The game project is in charge of integrating the engine and libraries.

### The Problems with Plugins

#### 1. Bottlenecks

As with anytime specifics and generics are mixed up, plugin systems create articifial limitations that would not have existed if the dependent project directly managed the plugins.  If a plugin were instead a general library being imported by the dependent project, that library could provide any sort of interface it wanted to perform any sort of operations on data passed to it.  The dependent project is free to interface the library with any aspect of the system.  But as a plugin, the library's only interface is through the hooks of the plugin manager.  There are an infinite number of possible hooks a plugin might need, and the plugin manager designers can only provide what hooks they expect to be the most common. 

#### 2. Plugin Conflicts

Due to SOC, plugins should not need to be concerned about other plugins.  A plugin that handles playing sound effects should not need to be concerned about a plugin that handles game logic.  At the same time, the plugin manager should not need to be concerned about the details of each plugin.  In essence, a plugin system is like a road where none of the drivers can see each other.  It's the blind leading the blind.

This eventually leads to conflicts.  One of the simplest cases is execution order.  A common method of implementing a plugin system is through hooks.  The plugin manager fires certain events that plugins can register handlers to be fired when that event occurs.  In order to do anything useful, these handlers are often modifying some shared state.  This can lead to race conditions where the handler for one plugin can overwrite the changes made by the handler of another plugin.  At this point the order of execution becomes crucial, where one plugin's handler needs to fire before another's.

When plugin systems face such conflicts, the only solution is to break SOC.  One example solution is for the plugin system to have a weighted hook system, where each plugin has the ability to designate whether a handler it is hooking into the system should be performed sooner or later. One method of implementing this approach is to split an event into multiple events.  "Initialize" could be divided into "Pre_Initialize", "Initialize", and "Post_Initialize".  A plugin that knows it creates problems when it fires a handler too early can hook into the "Post_Initialize" event, while a plugin that knows it creates a problem when it fires too late can hook into the "Pre_Initialize" event.  This solution is very brittle and creates to problems.  Firsttly, this approach is attemping to reduce conflicts by increasing granularity, but even with increased granularity, there is still a possibility that two handlers that need to hook into the "Pre_Initialize" event will conflict with each other.  Secondly, this solution requires plugins to be concerned with the other plugins in their ecosystem.  For a plugin to know it should register with the "Post_Initialize" event, it must be aware of how it could conflict with other existing plugins if it registered with the "Initialize" event.

In the real world, the solutions to plugin system conflicts are often less subtle.  It is not uncommon for plugin system ecosystems to grow in such a way that the most used plugins are hardcoded to play nicely with each other, throwing SOC out the window.

This dilemma is completely averted when dependents are driving dependencies. In that case a particular project is explicitly calling the handler functions of each of its dependencies and has complete control over the order of execution.  The specific project is the authority and arbitrator between each of its dependencies.  This enables the depenendencies to be safely be oblivious of each other.

### Plugin Popularity

So why are plugin systems used?

#### 1. End User Applications

The alternative to plugin systems (dependencies driving dependents) is only practical with software that is designed to be consumed by other software through an API. When creating end-user software, a plugin system is one of the the best options available for enabling a limited degree of extensibility.

Sometimes developers get accustomed to using plugin systems where plugins are actually the only good option and then carry that pattern to areas where better patterns exist.

#### 2. Convenience

Up front, a plugin system is more convenient to use.  Instead of having to manually integrate dependencies, the developer simply has to enable them.  But in the long run the cost of the plugin system's brittleness will outweight its short-term convenience.

#### 3. Pretension

Here is the common origin story of plugin systems. A developer creates a particular solution. Then the developer wants to make the solution more general so it can solve a wider variety of problems. 

The developer could divide the solution into smaller components that could each be individually reused.  In such a case the original solution would become decentralized. The attention that was once focused on a single solution would become divided amongst many smaller solutions.

Instead, the developer turns the particular solution into a plugin system. What once was a single solution is now the hub of an ecosystem. When dependents drive dependencies, the dependencies tend to get buried by the dependents.  But when one of the dependencies is a plugin manager, the plugin manager is always front and center.  In such a case the plugin manager is placed in control of the dependents not because it is qualified but because the developer is fixated on it as the most important piece of the puzzle.

Plugin systems are the lousy employee that becomes your boss because he's the CEO's nephew.

## Modal Parameters

There are two types of parameters: arbitrary and modal.  Arbitrary parameters are

Consider the following pseudo code.

```
foo(arg, toggle) {
    if (which == 1) {
        // Do A
    }
    else {
        // Do B
    }

    // Do more stuff
}
```

Here we have a function that is essentially three functions crammed into one.  The ```toggle``` parameter configures how the function operates.  That might not look like much of a problem, but
it breaks separation of concern, in that ```block A``` and ```block B``` are tightly coupled to each other and the ```toggle``` parameter.

The problem becomes accentuated when additional functionality is needed:

 ```
 foo(arg, toggle, second_toggle) {
     if (which == 1) {
         // Do A
     }
     else {
        if (second_toggle) {
            // Do B
        }
        else {
            // Do C
        }
     }

     // Do more stuff
 }
 ```

Now things are starting to get cramped.  This reliance on modal configuration does not scale.
```
foo(arg) {
    // Do A
    more_stuff(arg)
}

foo2(arg) {
    // Do B
    more_stuff(arg)
}

more_stuff(arg) {
  // Do more stuff
}
```

The second version is better.  Why?  Because it is more composable, has better separation of concerns, and can scale infinitely.

## The Override Pattern


Copyright 2018 By Christopher W. Johnson