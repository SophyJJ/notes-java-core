# Classes

- Template for creating an object
- Classes are reference types (that is, you can only access them by using a reference to them)

```java
// "Flight flight1" -> creates an object reference variable and tells it that it will hold a Flight reference
// "new Flight()" -> creates the Flight object in memory and returns a reference to that object
Flight flight1 = new Flight();

// flight2 will now point to the same object in memory as flight1 because it copies the reference
// the object in memory previously pointed by flight2 gets deleted
Flight flight1 = new Flight();
Flight flight2 = new Flight();

flight2 = flight1;
```

- encapsulation -> Goal is to hide the internal representation of the object
- access modifiers -> keywords to achieve encapsulation

## Access Modifiers

- no access modifier -> package private (public in package) -> use in classes and methods
- public -> available everywhere -> use in classes and methods
- private -> available only within class -> cannot be used in classes, can be used in methods

- class names have to match source class filename ONLY if the class is public

## Initializers

- You can iniitlaize a class in 3 ways:
  - field initializers
    - in the class, you can set an initial state for instance variables directly
    - you can set them to a value, reuse other variables, other classes' methods, etc
  - constructors
    - no return
    - java provides an empty constructor
    - if you create a constructor, then java will not provide the empty constructor anymore
    - `this(params)` will call the constructor with those params. You can chain them.
    - `this(params)` has to be the first line when chaining constructors
    - `private` constructors can only be called by other constructors
  - initialization blocks
    - shared accross all constructor
    - executed as if code was at start of each constructor
    - you can have multiple initialization blocks (they are exeucted in order)
    - runs after the field initializer
- instance variables always initialized to "zero" (ie, 0. 0.0. '\u0000', false, null)

## Parameters

- parameters are immutable = changes made to passed value are not visible outside of the method
- always passed by value (copy). It won't affect primitive types nor object reference vars.
- variable number of parameters:
  - ex:
    ```java
    // can only be used on the last parameter in the list
    // it's actually reading that last param as an array
    public void methodName(ClassName... paramList) {
        // handle paramList as an array
    }

     // call by passing an array
    instance.methodName(new ClassName[] { instance1, instance2, instance3 });

    // call by passing multiple params
    instance.methodName(instance1, instance2, instance3);
    ```

## Inheritance

- You can't override `final` or `private` methods from the BaseClass

### With Polymorphism

```java
/*
RULES:
  - inst CANNOT call new methods added ChildClass unless they override BaseClass'
  - *BAD* if you override a BaseClass instance var in ChildClass, then
    - if you call a BaseClass method, it WILL use the BaseClass intance var
  - *GOOD* if you override a BaseClass method in the ChildClass, then
    - if it will correctly call the ChildClass' version and use the correct instance var
    - if you call a BaseClass method that uses that overridden method, then it will correctly call the ChildClass' version
*/

BaseClass inst = new ChildClass();

// to call a ChildClass method (that wasn't overridden)
if (inst instanceof ChildClass) {
    ChildClass cc = (ChildClass inst);
    // NOTE: none of this is needed if calling an overridden method
    cc.childClassNewMethod();
}
```

### Without Polymorphism

```java
/*
RULES:
  - *Bad* if you override a BaseClass instance var in ChildClass, then
    - if you call a BaseClass method, it WILL use the BaseClass instance var
  - *GOOD* if you override a BaseClass method in ChildClass, then
    - if it will correctly call the ChildClass' version and use the correct instance var
    - if you call a BaseClass method that uses that overridden method, then it will correctly call the ChildClass' version
*/

ChildClass inst = new ChildClass();
```
- `@Override` will protect you at compile time
- All Clases (including Arrays) inherit from Object class

## Equality

- only way compare object reference vars's values is to override their `equals` method
- `==` will compare if they are pointing to the same object in memory
- the default `equals` takes the object they are pointing in memory into account

## super

- super treats the object as if it is an instance of the BaseClass
- useful for accessing BaseClass members that were overridden

## final

- prevents a member or class to be overridden or inherited

```java
// this class cannot be inherited from
final public class SomeClass {
}

// this class can be inherited from, but cannot override the method
public class SomeOtherClass {
    // this method cannot be overridden by children because it's final
    public final void methodCannotBeOverridden() {
    }

    // this method cannot be overridden by children because it's private
    private void methodIsPrivate() {
    }
}
```

## abstract

- the method HAS to be overridden
- if there is a method as `abstract`, then the whole class has to be `abstract`

```java
// the whole class has to be set as abstract if there is at least 1 abstract method
public abstract class SomeClass {

    // this method has to be overridden when inherited
    public abstract void someMethodToOverride();
}
```

# Constructors and inheritance

- constructors are *NOT* inherited. Every class is responsible for its own
- the ChildClass constructor always calls the BaseClass constructor (explicit or implicit)
  - if not specified, your ChildClass constructor will call the no-argument BaseClass constructor
- use `super` to call the BaseClass constructor. Has to be from the first line.
