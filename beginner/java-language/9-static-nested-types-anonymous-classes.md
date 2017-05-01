# Static Members, Nested Types, and Anonymous Classes

## Static Members (methods and fields)

- class member associated with the type and not the instance
- they can be accessed/ modified with the type
- all class instances access the same static member
- a static method does work specific to the class and not the instance
- static methods can only access static fields
- static members are created in separate memory than non-static members
- ex: static field: `static int var;`
  - non-static methods can access this + modify it
- ex: static method: `static int getVar()`
  - cannot access non-static members or fields
  - access it with: `ClassName.getVar();`
  - if you use static import, then you can just call it with `getVar()`
    - ex: `import static com.github.luiscarlin.ClassName.getVar();`

## Static Init

- type initializer, NOT instance init
- block gets run only the first time you use that class. No other ccalls needed.
- ex: `static {_}`
- declared outside of any other block
- cannot access instance members (non-static members)
- it has to handle all checked exceptions inside (cannot use `throws` clause)

## Nested types

- type (class/ interface) that's declared within another type
  - classes declared inside classes or interfaces
  - interfaces declared inside a classes or interfaces
- The nested type is a member of the enclosing type
  - nested type can access private members from the enclosing type
- nested types can be:
  - public -> available everywhere
  - package private (no modified) -> available in the package
  - private -> available ONLY in the enclosing type
  - protected -> available ONLY to children of the enclosing type
- 2 reasons to use them:
  1. Structure and scoping
    - see Static Nested Classes below
    - how to declare:
      - static class nested within classes
      - classes nested within interfaces
      - interfaces nested within classes or interfaces
  2. Inner Classes
    - See Inner Classes below
    - how to declare:
        - non-static classes nested within classes

## Static Nested Classes

- good for structure and scoping
- no relationship between instance of nested type and enclosing type
  - that means -> If does not have access to enclosing class members
- the class can be instantiated by itself by using `EnclosingClassName.StaticClassName`
- it's treated as a completely separate class (except for the name)
- useful when:
  - you just want to make nested type usable in some scenarios
  - you want to structure the nested type name relative to another class
ex:
```java
// define passenger with its rewards program
public class Passenger {
    // nested class is public, so it can be accessed from outside
    // since it's static, its name is scoped within the Passenger class
    public static class RewardProgram {
        private int level;

        public void setLevel(int level) { this.level = level; }
        public int getLevel() { return level; }
    }
    // make a way for people to access the reward program for this user
    private RewardProgram rp =  new RewardProgram();
    public RewardProgram getRewardProgram() {
        return rp;
    }
}
```
```java
// define crew with its rewards program  
public class Crew {
    public static class RewardProgram {
    }
}
```

```java
// how to use it
// as associated to an instance
Passenger steve = new Passenger();
steve.getRewardProgram().setLevel(3);

// since it's static, its name is scoped within the Passenger class
Passenger.RewardProgram platinum = new Passenger.RewardProgram();
platimun.setLevel(3)
```

## Inner Classes

- each instance of the nested class is associated with an instance of enclosing class
  - that means -> it has access to all members of the enclosing type
- non-static nested classes
- they are private
- cannot be accessed from the outside world
- can access members of enclosing type
- can only be used in the enclosing class because it's private
- when creating a new instance fo the inner class, it's associated with enclosing class
  - inner class has access to all members of enclosing class
  - inner class has `this` and `EnclosingClass.this` references

ex:
```java
public class Flight implements Comparable<Flight>, Iterable<Person> {
    private CrewMember[] crew;
    public iterator<Person> iterator() {
        return new FlightIterator();
    }

    // declared as private and non-static
    private class FlightIterator implements Iterator<Person> {
        private int index = 0;
        public boolean hasNext() {
            return index < crew.length;
        }
        public Person next() {
            Person p = crew[index];
            index++;
            return p;
        }
    }
}
```

## Anonymous Classes

- this is an inner class (private and non-static)
- it's a shortcut for using an inner class
- anonymous classes are created when they are used
- useful when you want to implemnent an interface or extend a class
- the anonyumous instance is associated with the containing class instance
  - that means -> has access to all members of the enclosing class
- Create it as if you are constructing an instance of the interface or base class

ex:
```java
public class Flight implements Comparable<Flight>, Iterable<Person> {
    private CrewMember[] crew;
    public iterator<Person> iterator() {
        // create the anonymous class as it's being used
        return new Iterator<Person>() {
            private int index = 0;
            public boolean hasNext() {
                return index < crew.length;
            }
            public Person next() {
                Person p = crew[index];
                index++;
                return p;
            }
        }
    }
}
```
