## Flat over Nested

> Flat is better than nested - The Zen of Python

### Rules

* Prefer flat logic over nested logic when organizing objects of the same level of specificity
  * In other words, minimize nesting except to nest general solutions within specific solutions
* When a problem requires nested logic, a nested solution can sometimes still employ flat data structures
  * For example, a DAG can be represented as a flat collection of references

## The Doctor's Dilemma

> There's more than one way to skin a cat

### Background

When there is damage inside a person's body, all health practitioners face the same challenge: the damaged area is surrounded by one or more layers that prevent direct interaction with the damaged area.  How does one get at the damaged area?

Some options are:

* Trigger chemical reactions
* Apply surface forces
* Cut them open

Systems need to be divided into layers.  It is unavoidable.  Even if a system is not divided into layers, it is probably built on top of other layers and other layers may be built on top of it.

Layers are a two-edged sword.  They compartmentalize, but also obscure.

### Rules

* Don't create tools that get in the way
* Minimize your layers, preferring [flat over nested](#flat-over-nested)
* Make the contents of your layers as accessible as possible
* Design with maintenance in mind, which often involves features that are only used for maintenance
