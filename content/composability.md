# Composability

##  Separation of Concerns

Complexity is just a bunch of simple.  No matter how large and complex a problem is, it can be cleanly solved if it is divided into enough smaller pieces.

However, the divisions cannot be arbitrary. Like chopping wood or carving a turkey, proper division of a complex problem requires dividing along existing lines. In a way, such division is simply accentuating existing lines.

A commonly used method of division is known as Separation of Concerns.  What is a concern? Within the context of software development, the definition of "concern" is fuzzy. Sometimes it is used to refer to a particular purpose, role, or domain. Dividing a system along such lines can be useful, but can also lead to equally fuzzy boundaries.

When attempting to understand and apply the concept of Separation of Concerns, it is more useful to define concerns and their boundaries through dependencies. When two components of a system have radically different dependencies or radically different dependents, that lends weight to keeping those parts separate. When two components of a system share similar dependencies and dependents, that lends weight to packaging those parts together.

While organizing the components of a system in such a manner does not reduce the dependencies of that system, it does reduce the dependencies for each component of the system.  This is good because

## Dependencies are Expensive

Dependencies are a two-edged sword. On one hand, everything except God Himself is dependent on something. Dependencies are essential.  But they are also expensive.

Dependencies add requirements to any component that depends on them. At minimum, dependencies and the requirement that they must be available. The component will not function as well or at all without its dependencies. Beyond that, dependencies can add additional requirements in the form of constraints. Constraints on how and where the component can be used. Some dependencies are incompatible with each other and force mutually exclusive selection.

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

##  Plugins

Instead of creating a particular component that manually includes and manages multiple dependencies, developers sometimes create a Plugin system to take the place of the particular component.

A Plugin system is a general component that manages a dynamic assortment of specific components.  A Plugin system puts dependencies in the drivers seat.

Ideally, individual plugins should be designed independent of each other.  That opens the possibility to have conflicts between plugins.  In order to resolve conflicts,

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


Copyright 2017 By Christopher W. Johnson