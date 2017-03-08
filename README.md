----------------------------------------------------------------------------------------------------------------
Title: The Abstract Factory Pattern

Sources:
Notes below regarding abstract factory pattern taken from "Design Patterns - Elements of Reusable Object-Oriented Software"
By Gamma, Helm, Johnson, Vlissides

Example Code provided by Derek Banas:
Tutorial: https://www.youtube.com/watch?v=xbjAsdAK4xQ
Source Code: http://www.newthinktank.com/2012/09/abstract-factory-design-pattern/

Author: Justin J

Purpose: FAU Object Oriented Software Design Course, Sprint 2017

----------------------------------------------------------------------------------------------------------------

Intent
- convert interface of a class into another interface clients expect
- lets classes work together that normally could not due to incompatible interfaces

Motivation
- sometimes a utility class (designed for reuse) is not compatible with a domain specific interface required by application
- we define a class so that it adapts a desired interface
	- inherit the subclass interface and adapted class's implementation
	- alternatively, compose subclass instance within the adapted class's implementation
- adapter is often responsible for functionality the adapted class doesn't provide
- adapter can fulfill desired responsibilities

Applicability
- when you want to use an existing class and its interface does not match the one required
- when you want to create a reusable class that cooperates with unrelated or unforeseen classes, classes that may not
  necessarily have compatible interfaces
- (object adapter only) when you need to use several existing subclasses, but it's impractical to adapt their interface by
  subclassing every one. object adapter can adapt the interface of its parent class

Structure
- see adapterpattern1.png

Participants
- Target
	- defines the domain specific interface that client uses
- Client
	- collaborates with objects conforming to the Target interface
- Adaptee
	- defines an existing interface that needs adapting
- Adapter
	- adapts the interface of Adaptee to the Target interface

Collaborations
- clients call operations on an Adapter instance, adapter in turn calls Adaptee operations to carry out request

Consequences
- class and object adapters have trade offs to consider
	- Class Adapter
		- adapts adaptee to target by committing to a concrete adaptee class. class adapter won't work when we want to adapt a
		  class and all of it's subcalsses
		- allows adapter to override some of adaptee's behavior, since adapter is a subclass of adaptee
		- introduces only one object and no additional pointer indirection is needed to get to the adaptee
	- Object Adapter
		- allows single adapter to work with many adaptees, adaptee itself and all of its subclasses
		- makes it harder to override adaptee behavior, requires subclassing adaptee and making adapter refer to the subclass
- need to consider how much adapting an adapter does
- a class is more reusable when you minize the assumptions other classes must make to use it
- two way adapters provide transparency, allowing two different clients to view an object differently

Implementation
- in C++ implementation of class adapter, adapter would inherit publicly from target and privately from adaptee
	- adapter would inherit publicly from target and privately from adaptee
	- adapter is subtype of target, but not of adaptee
- pluggable adapters - 3 methods of implementations
	- for all 3, find a narrow interface for adaptee, smallest subset of operations that allow us to adapt
	- abstract operations - define corresponding abstract operations for the narrow adaptee interface 
	- delegate objects - requests are forwarded to a delegate object
	- parameterized adapters - usual way to support pluggable adapters in smalltalk is to parameterie an adapter with one or more blocks

Related Patterns
- Bridge pattern is similar but different intent
- Decorator pattern
- Proxy pattern 