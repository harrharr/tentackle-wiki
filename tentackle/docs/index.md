# Introduction

This wiki describes the concepts, architecture and usage of the [Tentackle](https://tentackle.org)
Java application framework. Tentackle is open source, full-stack, opinionated and
available from [Maven Central](https://search.maven.org/search?q=tentackle).
Since it is a [modular](https://openjdk.org/projects/jigsaw/) framework,
the wiki is organized along its modules and maven plugins.

Tentackle is targeted to Java developers writing applications that are *not* primarily related to the web, 
which makes it pretty extraordinary, since the Java ecosystem became more and more web- and
data-oriented these days. Of course, non-web Java may be a small niche today, and so is the
audience for this wiki, probably.
That said, Tentackle solves many things fundamentally different compared
to the well-known mainstream frameworks. First and foremost, it moves the object-oriented
programming paradigm back into the spotlight. Working with real objects that represent state
*and* behavior, a.k.a. rich domain model, radically changes the way we're implementing the domain logic.
Most importantly, *any* of the domain methods can be invoked at *any* time, 
whether lazy loading from storage is necessary or not. You're not forced to provide 
workarounds for technical side effects such as LazyInitializationExceptions.
Moreover, since entities can freely travel between JVMs, lazy loading even works if the entity resides in a JVM, that is not directly connected
to a database, but is part of a network of JVMs, where one (or more) of them is responsible for the
persistence operations.
As a result, the main focus lies on the domain, but less on technical aspects such as persistence-, 
service- or view-layers.

This mindset borrows a lot from the way [Smalltalk](https://en.wikipedia.org/wiki/Smalltalk) 
worked back in the days. Of course, Java is not Smalltalk and Tentackle still uses databases
for persistence instead of the image-based approach. But with the help of Java interfaces, 
Tentackle hides the persistence implementation as much as possible from the domain logic.
In fact, entities *are* just interfaces. The separated implementations for the domain- and the 
persistence-logic are injected at runtime and have no dependencies to each other.
Since the domain- and persistence-implementations still reside within the 
same inheritance hierarchy of your domain-model (via their interfaces), there is no need for `instanceof`,
as opposed to the widely used [anemic model](https://martinfowler.com/bliki/AnemicDomainModel.html) 
approach with the domain logic implemented in a separate service layer.
Polymorhism just works as expected.

Furthermore, if you're familiar with [Domain Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design),
you will find some similarities in the way Tentackle deals with domain objects, and many of the classnames
and concepts will instantaneously make sense to you.
For example, component entities of an aggregate can only be persisted within the context of 
their root entity and when you're accessing such components within another 
[DomainContext](https://tentackle.org/static-content/sitedocs/tentackle/latest/tentackle-pdo/apidocs/org.tentackle.pdo/org/tentackle/pdo/DomainContext.html) than
the aggregate-root's context, those entities are automatically made immutable
to uncover programming errors as soon as possible ([fail-fast](https://en.wikipedia.org/wiki/Fail-fast)).

Finally, Tentackle itself is written the object-oriented way and can easily be extended
by your application. Large parts of the API are defined via interfaces and
only very few methods or classes are final. All factories
can be replaced easily via annotations. There is no *black magic* in terms of byte-code manipulation
and there is no classpath scanning. You don't need special plugins for your favorite IDE.
Everything is pure Java. Wherever appropriate, source code generation based on the domain model 
boosts your productivity and avoids programming errors.

Tentackle is different. It's *Java outside the box*.

## TL;DR
If you're developing Java applications that benefit from a rich, object-oriented domain model, this
document may be for you. Technical and scientific applications often do, 
as well as desktop (especially [JavaFX](https://openjfx.io/)) or distributed applications, 
where running the same domain logic at different physical locations/JVMs is an irrevocable requirement.
If you're looking for yet another web framework, this is definitely the wrong place.
