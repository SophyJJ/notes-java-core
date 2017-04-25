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
