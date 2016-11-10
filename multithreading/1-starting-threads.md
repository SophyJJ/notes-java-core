# Multithreading

## Starting Threads

- Thread = separate OS process
- You can run several in parallel with different priorities
- A new thread has the same initial priority as the parent
- 2 basic ways

### 1. Extend the Thread class in a subclass
- Thread is a class that has method `run()`
- Override that method
- You can also override the other Thread methods

```java
public class Runner extends Thread {
  public void run() {
    //code to run in parallel
  }
}

public class App {
  public static void main(String[] args) {
    Runner runner1 = new Runner();
    // if you call .run() then your code will run in the main thread
    // if you call .start() then run() will be run in its own thread
    runner1.start();
  }
}
```

### 2. Implement the Runnable interface
- Runnable is an interface with only method -> `run()` with no arguments
- Pass an instance of the implementation to an instance of Thread()
- If you want to override other Thread methods, then use method #1

```java
public class Runner implements Runnable {
  public void run() {
    //code to run in parallel
  }
}

public class App {
  public static void main(String[] args) {
    Thread t1 = new Thread (new Runner());
    t1.start();
  }
}

// Using an anonymous method.
// In this method, you don't need Runner class
public class App {
  public static void main(String[] args) {
    Thread t1 = new Thread (new Runnable() {
      public void run() {
        // your code to run in its own thread
      }
    });
    t1.start();
  }
}
```
