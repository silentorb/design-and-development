
## Hubs

Sometimes a system is designed in such a way that it is divided into many components with very clean separation of concern, and then all of those components are tied to a single "master" or "god" component.  Master components are like dieting during the weekdays and then ice cream binging over the weekend.

Master components usually have two problems:

    1. They have too many dependencies
    2. On top of connecting dependencies they add implementation logic.

The first problem can be solved by breaking up the Msater component into smaller pieces.  The second problem can be solved with the hub pattern.

A hub is a component with the following properties:

    1. It packages multiple dependencies.
    2. It contains little to no implementation logic.  It's simply a dumb package.
    3. It does not encapsulate it's dependencies.  (Though it could provide some additional shortcuts to aspects of its dependencies).

 The hub pattern divides components into two groups: hubs and implementation.  Either a component has many dependencies and little implementation logic or it has a lot of implementation logic and few dependencies.
