# Design Patterns

As the Gang of Four note in their book, there are
three types of design patterns:  
- **Creational patterns** deal with the creation of objects and instances.
- **Structural patterns** deal with the structure of classes and code.
- **Behavioral patterns** deal with the behavior of objects.


## [Builder Pattern](https://en.wikipedia.org/wiki/Builder_pattern)  
  - [List Builder Pattern – Unit Testing Object Hierarchies in C#](http://www.luckingtechnotes.com/list-builder-pattern-unit-testing-object-hierarchies-in-c/)  

## Inheritance
-	Inheritance is a core principle of OO programming  
    - Inheritance uses ‘IS-A’  
-	When you overuse inheritance, you can end up with designs that are quite inflexible and not amendable to change.  

## Composition  
- Composition uses ‘HAS-A’

## Design Principles (not patterns)
1.	Identify the aspects of your code that vary and separate them from what stays the same.  
    a.	Encapsulate what varies  
    *“Take the parts that vary and encapsulate them, so that later you can alter or extend the parts that vary without affecting those that don’t”*  
2.	Code to interfaces, not implementations  
    *“Program to an interface”* really means *“Program to a supertype”*  
    *“The declared type of variables should be a supertype, usually an abstract class or interface, so that the objects assigned to those variables can be of any concrete implementation of the supertype, which means the class declaring them doesn’t have to know about the actual object types”*  
3.	Favor composition over inheritance  
4.	
5.	Share common behavior via inheritance  
