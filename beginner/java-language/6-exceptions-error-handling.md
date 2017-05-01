# Exceptions and Error Handling

- programs should not have lots of if statements to check for errors because:
  - confusing & difficult for developers to remember to add them
- instead exceptions should be thrown and handled
- you can have embedded try/catch blocks inside other catch/finally blocks
- Error exceptions are thrown by the JVM about loading clases, etc
```
Object -> Throwable -> Error -> LinkageError, etc (unchecked exceptions)
                    -> Exception -> RuntimeException -> NullPointerException, etc (unchecked exceptions)
                                 -> IOException (checked exception)
                                 -> ...         (checked execption)
```

## Checked Exceptions

- they are checked by the compiler at build time
- very important exceptions
- Java won't let you compile if you don't have try/catch blocks for these
- they are children of the `Exception` class (omitting RuntimeException)
- custom exceptions you create are also Checked Exceptions

## Unchecked Exceptions

- they are not checked by the compiler
- Java lets you compile if you dont' handle them
- they are children of the `RuntimeException` class and children of the `Error` class

---

- catch more specific exceptions before more generic ones
- exceptions propagate up the call stack (accross method boudaries)
- instead of handling an exception, a method can let the exception occur and document it
  - `throws` clause is part of the method's signature
    - override this method, the new method in the child class has to be compatible with the base class
    - being compatible is important because other clases could be using polymorphism
      - `BaseClass bc = new ChildClass()`
      - Code using this would only know about the contract as it was defined in `BaseClass`
      - Compatibility prevents caller to face an exception they weren't expecting to catch
    - to be compatible, the ChildClass method should:
      - 1: not `throw` clause - meaning, it's handled within or not generated
      - 2: have `thow` clause to throw the same exception
      - 3: `throw` a derived exception from the base class
  - methods with `throws` in their signature tell the caller of the method that they need to handle it
  - these methods can still do try/finally to clean up

- if you rethrow an exception, make sure you include (wrap) the previous exception
  - use `initCause()` to include an exception into another one
  - some exception constructors allow you to associate some other exception with it
- Most of the time, you'll use an existing exception

## Custom Exceptions

- inherit from the Exception class (so they become checked exceptions)
- usually only have a contructor
- most of the functionality is inherited
- Need 2 constructors:
  - constructor with string for message
  - constructor with string and originating exception

```java
// Exception class
public class MyException extends Exception {
    public MyException(String message) {
        super(message);
    }
    public MyException(String message, Throwable cause) {
        super(message, cause):
    }
}

// class using the custom exception
public void methodThowing() throws MyException {
    // some code
    if (something == null) {
        throw new MyException("something was null");
    }

    try {
        // some code that could throw some exception
    }
    catch(NumberFormatException e) {
        throw new MyException("something was not a number", e);
    }
}

// class calling methodThrowing
public static void main() {
    SomeClass inst = new SomeClass();

    try {
        inst.methodThrowing();
    }
    catch(MyException e) {
        // getMessage() came from Exception class when we set it in the constructor
        System.out.println(e.getMessage( );

        // check if there was an originating exception
        if (e.getCause() != null) {
            System.out.println("Original exception" + e.getCause().getMessage());
        }
    }
}
```
