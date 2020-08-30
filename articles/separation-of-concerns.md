
##  Separation of Concerns

Complexity is just a bunch of simple.  No matter how large and complex a problem is, it can be cleanly solved if it is divided into enough smaller pieces.

However, the divisions cannot be arbitrary. Like chopping wood or carving a turkey, proper division of a complex problem requires dividing along existing lines. In a way, such division is simply accentuating existing lines.

A commonly used method of division is known as Separation of Concerns (SOC).  What is a concern? Within the context of software development, the definition of "concern" is vague. Sometimes it is used to refer to a particular purpose, role, or domain. Dividing a system along such lines can be useful, but can also lead to equally vague boundaries.

When attempting to understand and apply the concept of Separation of Concerns, it is more useful to define concerns and their boundaries through dependencies. When two components of a system have radically different dependencies or radically different dependents, that lends weight to keeping those components separate. When two components of a system share similar dependencies and dependents, that lends weight to packaging those components together.

While organizing the components of a system in such a manner does not reduce the dependencies of that system, it does reduce the dependencies for each component of the system.  This is good because [dependencies are expensive](./dependencies-are-expensive.md).
