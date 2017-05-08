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
  - `Future` interface
    - represents a thread result (returned by `myExecutorService.submit()`)
    - calling `get()`
      - block until task finished
      - return `Callable` interface result
      - throws `Callable` interface exception
