# Concepts

- Java's ecosystem became rather data-oriented nowadays, which is ok for most business applications (anemic model, service layer, micro services)
- some applications, however, benefit from a rich object-oriented domain model with inheritance and polymorphism. Those applications are mostly found in the technical or scientific domain.
- distributed computing (i.e. using the same domain-logic at physically separated places) is also an important issue for such applications.
- Completeness vs. Isolation vs. Performance: CIP theorem. (in analogy to the CAP theorem: Consistency vs Availability vs Partition-tolerance)
- example PLSBL isIngotReturned: requires domain- and persistence logic. Where to cut?
- unit- vs. integrations-tests
- PDO architecture (best of both worlds: rich model with strictly separated implementations of domain- and persistence logic whithin the same inheritance hierarchy. No instanceof in service layer)
- immutability as a key to correctness (PDOs selected outside the proper domain context are immutable by default)
- virtually always attached PDOs -> true OOP, no restrictions, life cycles, LazyInitializationExceptions. Methods can be invoked at any time! (hello again, Smalltalk ;))
- 