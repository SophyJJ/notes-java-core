# Multithreading

## Starting Threads

- Thread = separate OS process
- You can run several in parallel
- 2 basic ways

### 1. Extend the Thread class
- Thread is a class that has method `run()`
- Override that method

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
- Implement run()
- Pass an instance of the implementation to an instance of Thread()

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

// Using an anonymous method
public class App {
  public static void main(String[] args) {
    Thread t1 = new Thread (new Runner() {
      public void run() {
        // your code to run in its own thread
      }
    });
    t1.start();
  }
}
```
