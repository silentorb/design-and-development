# Project Longevity

## Performance

There is a saying in the programming world that "Premature Optimization is the root of all [kinds] of evil."  Premature optimization is a major pitfall, but deferring all concern for optimization can be a pitfall as well.  This is because all technology has a performance ceiling, and technical decisions can affect the height of that ceiling.  One of the easiest ways for a tool to support rapid development is to sacrifice performance.

Programming languages like C, C++, and Rust emphasize a principle known as Zero Cost Abstraction.  These are features that enhance development without effecting runtime performance.  Keep in mind that the cost referred to in Zero Cost Abstraction is simply runtime cost. ZCAs can add other types of costs, such as increased compile time or language complexity.

In essence, a ZCA is a higher level construct that seamlessly translates to a lower level construct, in such a way that the translation behavior can be predicted by the programmer.

One of the simplest Zero Cost Abstractions that most modern programming language have is...  