**Intent**

This page lists the gist of "SOLID" design principle for object-oriented programming. Most of the content were excerpted from [Object Mentor articles].

[[_TOC_]]

***

## SRP: The Single Responsibility Principle ##
**THERE SHOULD NEVER BE MORE THAN ONE REASON FOR A CLASS TO CHANGE.**

A **responsiblility** is "_a reason for change_". 

Because each responsibility is an axis of change. When the requirements change, that change will be manifest through a change in responsibility amongst the classes. If a class assumes more than one responsibility, then there will be more than one reason for it to change.

If a class has more then one responsibility, then the responsibilities become coupled. Changes to one responsibility may impair or inhibit the class’ ability to meet the others. This kind of coupling leads to fragile designs that break in unexpected ways when changed.

***
## OCP: The Open-Close Principle ##
**SOFTWARE ENTITIES (CLASSES, MODULES, FUNCTIONS, ETC.) SHOULD BE OPEN FOR EXTENSION, BUT CLOSED FOR MODIFICATION.**

Two primary attributes of modules that conform to the open-closed principle:

1. "**Open For Extension**". The behavior of the module can be extended. That we can make the module behave in new and different ways as the requirements of the application change, or to meet the needs of new applications.
2. "**Closed for Modification**". The source code of such a module is inviolate. No one is allowed to make source code changes to it.

**Abstraction is the Key.**


```cpp
typedef struct Shape *ShapePointer;
void DrawAllShapes(ShapePointer list[], int n)
{
  int i;
  for (i=0; i<n; i++)
  {
    struct Shape* s = list[i];
    switch (s->itsType)
    {
    case square:
      DrawSquare((struct Square*)s);
    break;
    case circle:
      DrawCircle((struct Circle*)s);
    break;
  } 
}
```

The function DrawAllShapes does not conform to the open-closed principle because it cannot be closed against new kinds of shapes.

###Strategic Closure###

The designer must choose the kinds of changes against which to close his design. 

####Using Abstraction to Gain Explicit Closure.####

In order to close DrawAllShapes against ordering, we need some kind of “ordering abstraction”. 

```cpp
class Shape {
  public:
    virtual void Draw() const = 0;
    virtual bool Precedes(const Shape&) const = 0;
    bool operator<(const Shape& s) {return Precedes(s);}
};
```

####Using a “Data Driven” Approach to Achieve Closure.####

###Heuristics and Conventions###
####Make all Member Variables Private.####
####No Global Variables -- Ever.####
####RTTI is Dangerous.####

***
## LSP: The Liskov Substitution Principle ##
**FUNCTIONS THAT USE POINTERS OR REFERENCES TO BASE CLASSES MUST BE ABLE TO USE OBJECTS OF DERIVED CLASSES WITHOUT KNOWING IT.**

Barbara Liskov:
> What is wanted here is something like the following substitution property: If for each object o1 of type S there is an object o2 of type T such that for all programs P defined in terms of T, the behavior of P is unchanged when o1 is substituted for o2 then S is a subtype of T.

####A Simple Example of a Violation of LSP####

```cpp
  void DrawShape(const Shape& s)
  {
     if (typeid(s) == typeid(Square))
      DrawSquare(static_cast<Square&>(s));
     else if (typeid(s) == typeid(Circle))
      DrawCircle(static_cast<Circle&>(s));
  }
```

####Square and Rectangle, a More Subtle Violation.####

```cpp
class Rectangle
{
public:
  virtual void SetWidth(double w)  {itsWidth=w;}
  virtual void SetHeight(double h) {itsHeight=h;}
  double       GetHeight() const   {return itsHeight;}
  double       GetWidth() const    {return itsWidth;}
private:
  double itsHeight;
  double itsWidth;
};
class Square : public Rectangle
{
  public:
   virtual void SetWidth(double w);
   virtual void SetHeight(double h);
};
void Square::SetWidth(double w)
{
  Rectangle::SetWidth(w);
  Rectangle::SetHeight(w);
}
void Square::SetHeight(double h)
{
  Rectangle::SetHeight(h);
  Rectangle::SetWidth(h);
}
```

####The Real Problem####

Validity is not Intrinsic. A model, viewed in isolation, can not be meaningfully validated. The validity of a model can only be expressed in terms of its clients.

####Design by Contract####

Meyer:

> ...when redefining a routine [in a derivative], you may only replace its precondition by a weaker one, and its postcondition by a stronger one.

Postcondition of `Rectangle::SetWidth(double w)`:
```cpp
assert((itsWidth == w) && (itsHeight == old.itsHeight));
```

***
## ISP: The Interface Segregation Principle ##
**CLIENTS SHOULD NOT BE FORCED TO DEPEND UPON INTERFACES THAT THEY DO NOT USE.**

The ISP acknowledges that there are objects that require non-cohesive interfaces; however it suggests that clients should not know about them as a single class.

###Interface Polution###

###Separate Clients mean Separate Interfaces.###
####The backwards force applied by clients upon interfaces.####

When we think of forces that cause changes in software, we normally think about how changes to interfaces will affect their users. However, there is a force that operates in the other direction. That is, sometimes it is the user that forces a change to the interface.

###Class Interfaces vs Object Interfaces###
####Separation through Delegation####
We can employ the object form of the `ADAPTER` pattern.
####Separation through Multiple Inheritance####


***
## DIP: The Dependency Inversion Principle ##

###Definition of a bad design.###

1. It is hard to change because every change affects too many other parts of the sys- tem. (Rigidity)

2. When you make a change, unexpected parts of the system break. (Fragility)

3. It is hard to reuse in another application because it cannot be disentangled from the current application. (Immobility)


###The Cause of “Bad Design”.###

* Rigidity is due to the fact that a single change to heavily interdependent software begins a cascade of changes in dependent modules. 

* Fragility is the tendency of a program to break in many places when a single change is made. 

* A design is immobile when the desirable parts of the design are highly dependent upon other details that are not desired.

###The Dependency Inversion Principle###

**1. HIGH LEVEL MODULES SHOULD NOT DEPEND UPON LOW LEVEL MODULES. BOTH SHOULD DEPEND UPON ABSTRACTIONS.**

**2. ABSTRACTIONS SHOULD NOT DEPEND UPON DETAILS. DETAILS SHOULD DEPEND UPON ABSTRACTIONS.**

A good example: `TEMPLATE METHOD` pattern from GOF book.
####Layering####
Booch:
> According to Booch , “...all well structured object-oriented architectures have clearly-defined layers, with each layer providing some coherent set of services though a well-defined and controlled interface.

####Separating Interface from Implementation in C++####
Use pure abstract class.


[Object Mentor articles]: http://www.objectmentor.com/resources/publishedArticles.html