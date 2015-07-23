##SOLID Object-Oriented Design Principles
|Principle|Description|Example and Related Design Patterns|
|:----|:----|:----|
|The Single Responsibility Principle (SRP)|THERE SHOULD NEVER BE MORE THAN ONE REASON FOR A CLASS TO CHANGE.|
|The Open-Closed Principle (OCP)|SOFTWARE ENTITIES (CLASSES, MODULES, FUNCTIONS, ETC.) SHOULD BE OPEN FOR EXTENSION, BUT CLOSED FOR MODIFICATION. ||
|The Liskov Substitution Principle (LSP)|FUNCTIONS THAT USE POINTERS OR REFERENCES TO BASE CLASSES MUST BE ABLE TO USE OBJECTS OF DERIVED CLASSES WITHOUT KNOWING IT.||
|The Interface Segregation Principle (ISP)|CLIENTS SHOULD NOT BE FORCED TO DEPEND UPON INTERFACES THAT THEY DO NOT USE.||
|The Dependency Inversion Principle (DIP)|A. HIGH LEVEL MODULES SHOULD NOT DEPEND UPON LOW LEVEL MODULES. BOTH SHOULD DEPEND UPON ABSTRACTIONS.<br/>B. ABSTRACTIONS SHOULD NOT DEPEND UPON DETAILS. DETAILS SHOULD DEPEND UPON ABSTRACTIONS.|Bridge Pattern<br/>Dependency Injection|

##Dependency Injection
Passing the service to the client, rather than allowing a client to build or find the service, is the fundamental requirement of the pattern.

|Category|Responsibility||
|:----|:----|:----|
|setter-based|client| the client exposes a setter method that the injector uses to inject the dependency|
|interface-based|service|the dependency provides an injector method that will inject the dependency into any client passed to it. Clients must implement an interface that exposes a setter method that accepts the dependency|
|constructor-based|constructor method|the dependencies are provided through a class constructor|

###4 elements:
1. the implementation of a service object; 
2. the client object depending on the service; 
3. the interface the client uses to communicate with the service; 
4. the injector object, which is responsible for injecting the service into the client. 


##Some Design Thoughts
###why do we inheritance?
1. to reuse code
2. for abstraction / dynamic binding / polymorphism

> inheritance represents an "is-a" relationship
> 
> reuse code from the base classes
> 
> apply the same class and methods to different data types
> 
> hierarchy is reasonably shallow and other developers are not likely to add many more levels
> 
> make global changes to derived classes by chaning a base class



##Reference
1. [When to Use Inheritance](https://msdn.microsoft.com/en-us/library/27db6csx%28v=vs.90%29.aspx)