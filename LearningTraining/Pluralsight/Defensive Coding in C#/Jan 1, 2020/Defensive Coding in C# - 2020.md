Jan 1, 2020  

# Defensive Coding in C# by Deborah Kurata
Resources: [https://github.com/DeborahK/CSharp-Defense](https://github.com/DeborahK/CSharp-Defense)  

Learn techniques for strengthening your application’s defenses against the perils awaiting it in the real world. You will see how to write clean code, create unit tests, build clear methods, and prepare for the unexpected.

Great applications perform required operations as expected, help users enter correct data, handle system and application exceptions, and make it easy for future developers to modify and maintain the code. Defensive coding focuses on improving code comprehension through clean code, improving code quality with unit tests, and improving code predictability by building clear methods and preparing for the unexpected. In this course, Defensive Coding in C#, you will gain the ability to strengthen your application’s defenses against the perils awaiting it in the real world. First, you will learn how to improve your code comprehension by following techniques such as the Single Responsibility principle. Next, you will discover how to improve your code quality through unit tests. Finally, you will explore how to improve your code predictability by validating method arguments, handling nulls appropriately, returning predictable results, and managing exceptions. When you are finished with this course, you will have the skills and knowledge needed to strengthen your code’s defenses.

## Why Defensive Code Matters  
__What Are We Defending Our Code From?__  
- Incorrect Entry  
  - Add Validation  
- Inalid Operations  
  - Check arguments  
  - Unit test operations  
- System mishaps  
  - Add checks  
  - Manage exceptions  
- Future Developers  
  - Write clean code  
  - Rerun unit tests  
  
__What is Defensive Coding?__  


>__[Defensive programming (coding)](https://en.wikipedia.org/wiki/Defensive_programming)__ is an approach to improve software and source code, in terms of:
>
>General quality – reducing the number of software bugs and problems.
>Making the source code comprehensible – the source code should be readable and understandable so it is approved in a code >audit.
>Making the software behave in a predictable manner despite unexpected inputs or user actions. - Wikipedia  

__Defensive Coding Helps Us Improve:__
- Code comprehension 
- Code quality  
- Code predicability  

__Competing Goals:__
- INCREASE CODE: Improving code predictability by __writing more validation and exception management code__  
- REDUCE CODE: Improving code comprehension by __eliminating unnecessary code__  

__Fitness for a Purpose__  
__Risk vs. Defenses__  

---

__Course Overview__

__Strengthening our defenses__
- Code comprehension  
- Code quality  
- Code predictability  

__Validating method arguments__  

__Handling nulls__  

__Returning predictable results__  

__Managing exceptions__  

---  
## Strengthening Our Codes Defenses  

__Evaluating Weaknesses__
- Identify Potential Weaknesses  
  - Code was Copy/paste  
  - Presentation logic mixed with business logic  
  - Difficult to unit test  
  - No validation  
  - No exception handling  
  
__Code comprehension__  
- Easy to read  
- Have a clear intent  
- Simple  
- Thoughtful  

>__Refactoring__ is the process of restructuring code, altering it's organization without changing its behavior.

__Improving Code Comprehension__  
- Single responsibility principle  
- Separation of concerns  
- Don't repeat yourself (DRY)  

__Single Responsibility Principle__  
- Single focus  

__DEMONSTRATION:__  
Show simple example of exctracting code into single focus tasks.  
- Calculate profit margin  
- Check the profit margin  
- Save the new price information  

__Naming Convention for exctracted code__
- Since methods perform __actions__ the method name shoudl eb a __Verb__ with and option subject that __Verb__ is acting on.
  - Examples:
    - CalculateMargin
    - CheckMinimumMargin
    - SavePrice

__Separation of concerns__  
- Separating an application into distinct parts where each part addresses a specific concern or aspect of the application. This is often done with __domains__ or __layers__.  
  - __Presentation layer__ - for user interface and visual appearance  
  - __Business Logic or Services Layer__ - for the logical calcualtions and operations of the application  
  - __Data layer__ - for the collection of data and interface to the data stores  






































