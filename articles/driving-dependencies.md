
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
