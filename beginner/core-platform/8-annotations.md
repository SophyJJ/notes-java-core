# Annotations

- special types that act as metadata
- they must be interpreted by tools or execution environments
- annotations are read at compile time
- java comes with some annotations: `@Override`, `@Deprecated`, etc
- you can also create your own custom annotations
- ex:

```java
// you can pass retention policies for source/ class / runtime (loads into runtime)
// source: exists only in source file and dropped by compiler
// class: compiled into the class file, but dropped at runtime
// runtime: loaded into runtime and accessible with reflection
@Retention(RetentionPolicy.RUNTIME)
// allow only oon classes
@Target(ElementType.TYPE)
public @interface WorkHandler {
// you can pass elementes
    boolean runAsThread() default true;
}

// use
@WorkHandler(runAsThread = false)
public class SomeClass ... {
//...
}
```

- you can also use reflection with the annotation to see if values have been set
- if you specify the element `value()` then you don't have to specify the element name in the annotation
- possible elements: primititve, string, Enum, Annotation, Class<?>, array

```java
// create annotation
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface ProcessedBy {
    Class<?> value();
}

// annotate a class
// this target class can be processed by AccountWorker
// ActionWorker implements TaskWorker
@ProcessedBy(AccountWorker.class)
public class BankAccount {
    public BankAccount(String id) {}
    ...
}

// read value of element and act on it
void startWorkSelfContained(Object workerTarget) throws Exception {
    // this returns instace of BankAccount
    Class<?> targetType = workerTarget.getClass();
    // do reflection on the annotation used in the BankAccount class
    ProcessedBy pb = targetType.getAnnotation(ProcessedBy.class);
    // obtain the worker that's allowed to do work on this target class
    Class<?> workerType = pb.value();
    // instantiate a new worker
    TaskWorker worker = (TaskWorker) workerType.newInstance();
    // do work
}

// start it
BankAccount acct1 = new BankAccount();
startWorkSelfContained(acct1);
```
