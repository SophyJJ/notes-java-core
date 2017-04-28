# Exceptions and Error Handling

- programs should not have lots of if statements to check for errors because:
  - confusing & difficult for developers to remember to add them
- instead exceptions should be thrown and handled
- you can have embedded try/catch blocks inside other catch/finally blocks
- Error exceptions are exceptions thrown by the JVM about loading clases, etc
```
Object -> Throwable -> Error -> LinkageError, etc (unchecked exceptions)
                      -> Exception -> RuntimeException -> NullPointerException, etc (unchecked exceptions
                                   -> IOException (checked exception)
                                   -> ...         (checked execption)
```
