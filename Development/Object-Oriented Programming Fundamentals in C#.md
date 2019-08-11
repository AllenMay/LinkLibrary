# Core Principle of Object Oriented (OO) Programming  
## Encapsulation  
## Inheritance  
## Interfaces  
## Extension Methods  
  
Notes from “[Object-Oriented Programming Fundamentals in C#](https://app.pluralsight.com/library/courses/object-oriented-programming-fundamentals-csharp/table-of-contents)”   
by Deborah Kurata ( Pluralsight )  
  
__Four Pillars of OOP__  
  - Abstraction
  - Encapsulation
  - Inheritance
  - Polymorphism
  
__Constructor__  
A special method of a class or structure in object-oriented programming that initializes an object of that type.  
  
__Key Steps__  
  - Identifying Classes
  - Represents business entities
  - Defines properties (data)
  - Defines methods (actions/behavior)  
  
__Separating Responsibilities (Separation of Concerns)__
  - Minimizes coupling  
    - The degree to which classes are dependant on each other  
    - Low coupling makes better testability and maintainability  

__Maximizes cohesion__
  - The measure of how related everything in a class is to the purpose of the class
  - High cohesion makes the class easier to maintain and test  

__Simplifies Maintenance__
  - Improves Testability  

__Establishing Relationships__  
  - Define how objects work together to perform the operations of the application  
    - Defining relationships  
    - Types of relationships  
    - Collaboration (“uses a” relationship)  
    - Composition (“has a” relationship)
      - Aggregation is a special type of composition where by the component parts do not exist except as part of the composition  
    - Composition: References
    - Composition: Ids
    - Inheritance (“is a” relationship)

__Leveraging Reuse__
  - Involves extracting commonality
  - And building reusable classes/components
    - Build it once
    - Test it once
    - Update it once
    - Enhance it once

__NOTE:__ By convention, the class responsible for retrieving and saving the data for an entity is called a ‘Repository Class’

__Design Pattern:__ Repository Pattern




## Encapsulation
(top)


## Inheritance 
(top)


## Interfaces
__Understanding Interfaces__  
- Class Interface
- Interface Metaphors
- Defining an Interface
- Implementing and Interface
- Interface-based Polymorphism  
 __Benefits of Interfaces and Polymorphism__  
   - Strong typing
   - Defines commonality among unrelated classes
   - Aids in building generalized utility methods with class-unique functionality


## Extension Methods
(top)


## Final Words and Next Steps
__Indentifying Classes__  
When given a specification for a feature or a new application start by identifiying the classes from the requirements source specification.
- __Represents business entities__ - Object-oriented programing represents the entities and concepts of an application as a set of classes. 
- __Defines properties (data)__ - Each class has properties that define the data each object will manage. 
- __Defines methods (action/behavior)__ - Each class has methods, which are the actions and behaviors that each object can perform. Then analyze the classes you identified and separate responsibilites as needed.

__Separating responsibility__
- __Minimizes coupling__ - Minimize coupling by ensuring each class has a single purpose.
- __Maximies cohesion__ - Maximize cohesion by reviewing the properties and methods of each class to confirm each one belongs to that class.
- __Simplifies maintenance__ - Single-focus classes simplify maintenance and improve testablity
- __Improves testability__ - 

__Establishing relationships__
- Defines how objects work together to perform the operations of the application

__Leveraging reuse__
- Involves extracting commonality
- Building reusable classes / components
- Defining interfaces

