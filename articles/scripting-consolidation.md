# Scripting Consolidation

## Big Fish, Small Pond

* At the time of this writing, the Tiobe index ranks Python as the most popular programming language
  * The Tiobe index's ranking system skewed but still useful
  * Redmonk uses a more balanced rating system
* Some may think that Python's popularity is an indicator that scripting languages are becoming more popular
* It's not—scripting language use is diminishing
* The scripting town has grown smaller and is no longer big enough for so many scripting languages
* Python is the most practical general-purpose scripting language and is rising above its peers because of that

## The Shift

* The problem with weak-typed, dynamic, interpreted scripting languages is they have a low ceiling
* As time has passed, there hasn't been much that can be significantly improved with scripting language implementations and tooling
* In contrast, static, strong-typed compiled languages:
  * Have a much higher ceiling of potential
  * Have continued to advance
  * Have plenty of room for more improvement
* The distinctive advantages of scripting languages are gradually becoming less distinctive

## Shrinking Gaps

* Here are some of the cases where compiled languages have grown while scripting languages have grown less

### Type Annotations

* A classic benefit of scripting languages is they don't need type annotations
* Type inference has reduced the need for type annotations
  * Type inference is continuing to improve
* Improved generics results in more flexible code that further needs less type annotations
* Haskell is a showcase example of how well a language can work with advanced type inference and generic functions

### Tooling

* Strong typing and static logic support robust tooling
* Dynamic typing and non-deterministic logic limits what tooling can do
* Static languages are benefiting from ever more advanced intellisense and refactoring tools
* Dynamic language tooling is improving as well but at a slower, more limited pace

### Improved Compile Times

* Build times have been a traditional weakness of compiled languages
* Incremental builds and hot-swapping are gradually reducing build times
* In increasingly more cases, built times are becoming trivial

### REPL

* Scripting languages use to be one of the only means of rapid development where a programmer could receive immediate feedback to code changes
* In part due to decreased build time and also in light of run time improvements (particularly JIT), it is becoming easier to perform rapid development with a static language, where a developer can write code and see immediate results

### Meta-Programming

* Most scripting languages excel at meta-programming
* Meta-programming cannot be statically resolved and must be resolved at runtime, making it the bane of security, code review, and tooling
* Meta-programming is mostly used to work around limitations in a programming language
* As programming languages advance, there is less need to rely on meta-programming for workarounds

## Python's Strengths

* Here are some notable causes of Python's popularity:

### Simplicity

* Python is not as simple or uniform as advertised, but unlike many of its competitors it at least *tries* to be

### The Mullet Language

* > Business in the front, party in the back

* Python has an implicit philosophy: "Be formal and disciplined where you can—hack everything else to the moon"

* Most programming languages falls somewhere along the spectrum of corporate and hacker

* Python has done a remarkable job of straddling that line

* On one end of the spectrum, Python has some of the most polished specs and conventions in the form of its PEP documents

* On the other end of the spectrum, official Python libraries employ some of the most eye-watering hacks one can find in a major programming language

  * Hacks usually employed in order to maintain compatibility *with itself*

* Extreme pragmatism has helped more than hindered Python's adoption

### Islands

* One of the little-known secrets of the Python ecosystem is it is one of the most fragmented software ecosystems
* Many Python developers work within a single domain, and would be surprised at how different and incompatible the other Python domains are from their own
* While Python fragmentation causes many problems, it is also an essential ingredient for Python's proliferation
* Python is like a Chameleon, adapting to each environment as needed without forcing every other use-case of Python to work identically

### The Servant Language

* Python is a humble language, ready to serve
* Instead of trying to force everyone to play by its terms, Python is one of those technologies that is eager to meet others where they are at
* While not as easy to embed as Lua, Python is still one of the nicest programming languages to embed into a native application

## Scripting Language Showdown

* Below is a list of major scripting languages and why they are not competition for Python
* Most of their current use is due to legacy momentum

### Perl

* Perl bet on the horse of, "There's more than one way to do it"
* That horse only had three legs and lost the race
* Perl is convoluted and needlessly difficult to learn

### Ruby

* Ruby was designed to be fun
* Python was designed to be practical
* Ruby and Python are too similar and redundant to indefinitely compete in a shrinking space
* In the programming world, practical trumps fun
* As with [the ant and the grasshopper](https://read.gov/aesop/052.html), in the long run practical is usually more fun

### Lua

* Lua has maintained a niche as *the* lightweight embedded scripting language
* Python is not as lightweight, but is actually embedded into far more applications than Lua
* Lua is going strong for now but minor environmental changes could tip the balance and cause Python to consume Lua's market

### VBScript

* Not even Microsoft wants VBScript

### PHP

* PHP's main strength used to be that it is a domain-specific language
* Server architecture has grown and abstracted to the point where PHP's domain-specific features are antiquated
* Modern PHP frameworks hardly leverage PHP's domain specific features anymore
* At this point PHP is a domain-specific language used like a general-purpose language
* Python does general-purpose better

### JavaScript

* JavaScript is the scripting language that doesn't want to be a scripting language anymore
* Gone are the days of code littered with browser-compatibility hacks
* Gone are the days when the measure of a JavaScript developer was how much magic he could perform through class prototyping
* Being the language of the web, the world has needed to get on the same page on every major issue of JavaScript, which has forced the JavaScript ecosystem into a very cautious, globally-aware mentality
  * Every other software ecosystem can afford to have more islands than JavaScript
* The modern JavaScript ecosystem is often as formal and disciplined as Java
* JavaScript is the most transpiled-to programming language, with less and less JavaScript developers actually writing JavaScript
* TypeScript is the new JavaScript
* TypeScript will probably replace JavaScript

