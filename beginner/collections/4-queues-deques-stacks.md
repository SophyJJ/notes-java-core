# Queues, Deques, and Stacks

- collections with modification order
- you can also set a priority on items to be taken out of the queue

## Queues

- First In, First Out
- you can have a bounded queue, where no new elements can be placed in the queue until other ones are removed
- there are 2 versions for adding, pulling, and peeking. One set of versions throws exceptions in edge scenarios

## Priority Queues

- order in which things comes out is based on priority of elements rather than when they were added
- you would need to specify a Comparator

## Stacks and Deques

- Last In, First Out
- Top element is popped off
- Java.Util.Stack deprecated -> Don't use it
- Instead of Java.Util.Stack, use Deque (double ended queue)
- You can use Deque as a queue or as a stack. (ie. you can add/ remove from head/tail)
- If you want to use it as a stack, you can use `push` and `pop` if you want


---

- Avoid using LinkedList as queue and Java.Util.Stack
- LinkedLists are good for random access, and it would defeat the purpose of using it as a queue
- Also, LinkedList allows null elements, which may confuse your program (usually null would represent that no elements are present)
