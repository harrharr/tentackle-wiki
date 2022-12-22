# Introduction

This wiki describes the concepts, architecture and usage of the [Tentackle](https://tentackle.org)
Java application framework. Tentackle is open source, full-stack, opinionated and
available from [Maven Central](https://search.maven.org/search?q=tentackle).
Since it is a [modular](https://openjdk.org/projects/jigsaw/) framework,
the wiki is organized along its modules and maven plugins.

Tentackle is targeted to Java developers writing applications that are *not* primarily related to the web, 
which makes it pretty extraordinary, since the Java ecosystem became more and more web- and
data-oriented these days. Of course, non-web Java is just a small niche today, and so is the
audience for this wiki, probably.
That said, Tentackle solves many things fundamentally different compared
to the well-known mainstream frameworks. First and foremost, it moves the object-oriented
programming paradigm back into the spotlight. Working with real objects that represent state
*and* behavior, a.k.a. rich domain model, radically changes the way we're implementing the domain logic.
Because any of the domain methods can be invoked at any time, whether lazy loading from storage
becomes necessary or not, you will no more care about boring LazyInitializationExceptions. 
This even works if the object resides in a JVM, that is not directly connected
to a database, but is part of a network of JVMs, where one (or more) of them is responsible for the
persistence operations. You simply focus on objects, not on technical aspects such as persistence-, 
service- or view-layers.

This mindset borrows a lot from the way [Smalltalk](https://en.wikipedia.org/wiki/Smalltalk) 
worked back in the days. Of course, Java is not Smalltalk and Tentackle still uses databases
for persistence instead of the image-based approach. But with the help of Java interfaces, 
Tentackle at least hides the persistence implementation as much as possible from the domain logic.

Furthermore, if you're familiar with [Domain Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design),
you will find some similarities in the way Tentackle deals with domain objects, and many of the classnames
will instantaneously make sense to you.
For example, when you're accessing components of an aggregate within another `DomainContext` than
the aggregate-root's context, those components are automatically made immutable.

Finally, Tentackle itself is written the object-oriented way and can easily be extended
by the application. Large parts of the API are defined via interfaces and
only very few methods or classes are final. All factories
can be replaced easily via annotations. There is no *black magic* in terms of byte-code manipulation
and there is no classpath scanning. You don't need special plugins for your favorite IDE.
Everything is pure Java. Wherever appropriate, source code generation based on the domain model 
is used to boost your productivity and avoid programming errors.

It's different. It's Java outside the box.

## TL;DR
If you're developing Java applications that benefit from a rich, object-oriented domain model, this
document may be for you. Technical and scientific applications often do, 
as well as desktop (especially [JavaFX](https://openjfx.io/)) or distributed applications, 
where running the same domain logic at different physical locations/JVMs is an irrevocable requirement.
If you're looking for yet another web framework, this is definitely the wrong place.
