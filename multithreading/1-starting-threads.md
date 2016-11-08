# Multithreading

## Basic Thread Synchronization

- 2 kids of problems when multithreading: data caching and threads interleaving

### 1. Caching Variables and `volatile`
- variables' values may get cached by default because threads may not expect them to change on their own.
- For optimization, Java may cache values because it won't expect threads to interact
- So, if you have 2 threads setting or getting the same variables, then you should use `volatile`
- `volatile` is used to prevent threads to cache a variable that is not modified by the thread

```java
// Example:
// In this example two threads interact with the variable "running".
// For this reason, that variable was declared "volatile"
public class Processor extends Thread {
  // "volatile" = this variable should not be cached by any thread
  private volatile boolean running = true;

  // this will be run in its own thread when calling .start()
  public void run() {
    // reading "running". Since this thread never changes "running", then
    // it could be cached during Java optimization. For this reason, we need
    // to declare it as volatile
    while (running) {
        System.out.println("hello");

        try {
          Thread.sleep(100);
        }
        catch(InterruptedException e) {
          e.printStackTrace();
        }
    }
  }

  public void shutdown() {
    // this will stop the running thread
    running = false;
  }
}

public class App {
  // the main thread interacts with "running" variable too
  public static void main(String[] args) {
    Processor proc1 = new Processor();

    // this calls "run()" in its own thread
    proc1.start();

    // this pauses the main thread until some input is given
    System.out.println("Press return to stop...");
    Scanner scanner = new Scanner(System.in);

    // set the volatile variable to stop the proc1 thread
    proc1.shutdown();
  }
}
```
