# Multithreading and Concurrency

- Process:
  - instance of a program/ application
  - when started, resources (memory, etc) are allocated and given to the process to use
  - starts with only the Main thread
  - can run multiple threads

- Thread
  - sequence of programmed instructions
  - what actually executed your program's code
  - uses the processes resources (memory, etc)
  - can spin up other threads

- Multithreading
  - a process running multiple threads at some point in time
  - allows better use of CPU while threads waiting on resources
  - reduces wall-clock time for a program execution
  - you must break the problem in parts to be able to run in parallel
  - you can create and coordinate manually (Direct) or you can use Java's higher abstractions

- Concurrency
  - running concurrent operations/ executions within a process
  - without coordination, threads could act erraticaly when using same resources  

### Direct Thread Handling

- most basic thread handling
- you start a thread on a task -> thread terminates at the end of it
- you are responsible for coordinating between threads
- exceptions are tied to the thread -> each thread has to handle their own exceptions
- Start a thread
  - implement the `Runnable` interface
    - override the `run` method. This method is a task to be run in the thread
    - within the method, you have to handle ALL exceptions
  - use the `Thread` class
    - represents the thread so we can control it (start, stop, coordinate)
    - the constructor expects an instance that implements `run()` from `runnable`
    - call `myThread.start()` to start the thread execution
    - call `myThread.join()` from calling thread to block (wait) until `myThread` terminates

### Thread Pools

- java abstraction to facilitate working with threads
- creates a queue for tasks
- assigns tasks to run in a pool of threads
- handles detials of managing threads
- 2 types to deal with thread pools
  1. `ExecutorService` interface
    - you submit tasks to its queue, and it will schedule/ manage them for you
    - `myExecutorService.submit()`: submits an instance of a class (implements runnable) into the thread pool
    - `myExecutorService.shutdown()`: finish current work, but don't accept new tasks in the queue
    - `myExecutorService.awaitTermination(60, TimeUnit.SECONDS)`: wait
    -
  2. `Executors` class that implements `ExecutorService` interface
    - creates thread pools
      - static or dynamic size
      - schedule tasks for a later time

## Returning values/ noticing exceptions into caller threads

- If handling manually, child thread would have to save return values/ exception info in memory, and caller read from memory
- If using higher abstraction:
  - `Callable` interface
    - replaces the `Runnable` interface
    - override `call`. It can return values/ throw exceptions
  - `Future` interface to harvest results
    - represents a thread result (returned by `myExecutorService.submit()`)
    - calling `get()`
      - block until task finished
      - return `Callable` interface result
      - throws `Callable` interface exception

## Concurrency Issues

- occurs when threads write on shared resources (memory, etc)
  - writes need to be coordinated
    - if not coordinated, program can crash or generate wrong results
- not an issue if threads only read from shared resources
- problem happens because of non-atomic operations
  - ex: `amount += balance;` is not atomic. It's actually 3 steps
    - read current value from mem -> perform addition -> write result to memory

## Synchronized methods

- goal: to coordinate thead access to methods in a class
- it manages concurrrency by using a lock for each object instance
- you use the `synchronized` method modifier in as many methods as you want per class
  ex:
  ```java
  public synchronized void readOrWriteOperationMethod() {
    // only one thread can run this method at a time
    // also blocks other synchronized methods in this instance
  }
  ```
- synchronization managed per instance.
  - No more than ONE thread can run ANY ONE synchronized method at a time for that instance
- use synchornized to:
  - protect writing into memory by multiple threads
  - reading a value that might be modified by another thread
- it carries significant overhead
- constructors never synchronized (because always run by 1 thread at isnatnce creation)

## Manual Synchronization (synchronized blocks)

- all java objects have locks
- you can use synchronized statement blocks
  - no need to have synchronized methods. Now, you can get locks for any method
  - ex:
    ```java
    synchronized(myObjectInstance) {
      // the thread gets a lock on myObjectInstance
      // this is run atomically per thread per instance
      myObjectInstance.readOrWriteOperationMethod();
    }
    ```
- advantage: you can use non-thread save classes in a secure way
  - also, while a `synchronized` method is safe, calling several of them in a block may not
  - sometimes a block of synchronized methods needs to be be atomic. Use `synchronized` block
- locks are placed on an instance such that only 1 thread can access a synchronized method
- ex:
  ```java
  synchronized(myInstance) {
    // lock on myInstance obtained. Only this thread can execute any methods (even sync) on this instance
    myInstance.someSynchronizedMethod();
    myInstance.someNonSyncrhonizedMethod();
    myInstance.someOtherSynchronizedMethod();
    // the block is thread safe even if some methods are not
    // the block is run atomically
  }
  ```

## Concurrency and Collections

- most collections are not thread safe
- use thread-safe wrappers (Collection class static methods)
  - `synchronizedList(myListInstance)`, `synchronizedMap(myMapInstance)`, etc
- when you use the wrapper:
  - actual work -> done by original instance of collection
  - synchronized work -> done by wrapper

## Blocking Queues

- used when coordinating producer/ consumer work
  - producer: generates some data and makes it available
  - consumer: reads the data and does operations on it
    - must wait until producer is done generating the data to operate on it

- you can use a blocking queue:
  - `LinkedBlockingQueue`, `PriorityBlockingQueue`
  - with it, the consumer will attempt to read from the queue, and block if no data to read
    - when data becomes available, the consumer will wake up and start it's work on the data

## Other

- `java.util.concurrent`
  - has lots of types to manage concurrency
  - ex: semaphores -> coordinate access to multiple resources
- `java.util.concurrent.atomic`
  - provides atomic wrappers for primitives
  - atomic operations on variables. Ex: set, get, getAndAdd, etc.
