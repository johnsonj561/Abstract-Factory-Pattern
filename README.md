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
- provides an interface for creating families of related or dependent objects without specifying their conrete class

Also Known As
- Kit

Motivation
- clients are not aware of the concrete classes they're using
- enforces dependencies between the concrete classes

Applicability
- use when system should be independent of how its products are created, composed, and represented
- when a system should be configured with one of multiple families of products
- when a family of related product objects is designed to be used together, and you need to enforce this constraint
- when you want to provide a class library of products, and you want to reveal just their interfaces and not implementations

Structure
- see AbstractFactoryPattern.png

Participants
- AbstractFactory
	- declares the interface for operations that create abstract product objects
- ConcreteFactory
	- implements the operations to create concrete product objects
- AbstractProduct
	- declares an interface for a type of product object
- ConcreteProduct
	- defines a product object to be created by the corresponding concrete factory
	- implements the AbstractProduct interface
- Client
	- uses only interfaces declared by AbstractFactory and AbstractProduct classes

Collaborations
- normally a single instance of a ConcreteFactory class is created at run time
	- this concrete factory creates product objects having a particular implementation
	- to create different pdocut objects, client should use a different concrete factory
- AbstractFactory defers creation of product objects to its ConcreteFactory subclass

Consequences
- isolates concrete classes - helps control the classes of objects that an application creates
	- isolates clients from implementation of classes, clients manipulate instances through their abstract interfaces
- makes exchanging product families easy
	- class of concrete factory appears only once, where it's instantiated, makes it easy to change the concrete factory being used
	- allows for different product configurations simply by changing the concrete factory
- promotes consistency among products
- supporting new kinds of products is difficult - extending abstract factories to produce new kinds of products isn't easy

Implementation
- Factories as singletons - best implemented as a Singleton because applications only need 1 instance
- Creating the products - AbstractFactory only declares interface for creating the products, up to ConcreteProduct subclasses to actually create them
	- most common technique is to define a factory method for each product
	- concrete factory will specify its products by overriding the factory method for each
- Defining extensible factories - AbstractFactory usually defines a different operation for each kind of product it can produce
	- kinds of products are encoded in the operation signatures
		- adding new kind of product requires changing the AbstractFactory interface and all classes dependent
		- less safe design is to add parameter to operations where parameter specifies the object to be created

Related Patterns
- Often implemented with Factory Method
- Concrete Factory is often a singleton