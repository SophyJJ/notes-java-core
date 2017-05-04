## Collections

- Arrays are statically sized, have explicit positioning, very basic
- Collections are iterable, provide type safety, and can dynamically change its size
- if something uses generics, that means that caller can set type for it
- Most collections (except Map) implement the Collection interface
- Collection interface:
  - implements iterable
  - provides common methods:
    - size, clear, isEmpty, add, addAll, conatins, remove, retainAlll
  - some depend on equals method
- printing all elements with lambda expressions:
  - `myList.forEach(m -> System.out.println(m.getLabel()));`
- remove elements that match a predicate
  - `myList.removeIf(m -> m.getValue().equals("abc"));`
- convert collection to array
  - `MyClass[] a1 = myList.toArray(new MyClass[0]);`

## Common Collection Interfaces

- Collection: Basic collection operations
- List: Collection with order
- Queue: Collection with order and "head" element
- Set: Collection with no duplicates
- SorftedSet: set with sorted elements

## Common Collection Classes

- ArrayList: a List
  - Backed by: resizable array
  - Efficient: random access
  - Inefficient: random inserts
- LinkedList: a List and a Queue
  - Backed by: doubly-linked list
  - Efficient: random insert
  - Inefficient: random access
- HashSet: a Set implemented as Hash table (dict) (uses hash values of elements)
  - Efficient: for general purpose at any size
- TreeSet: a SortedSet implemented as balanced binary tree
  - Efficient: in-order access
  - Inefficient: less efficient than HashSet to modify and search

## Sorting

- 2 ways to specify sort: `Comparable` anb `Comparator` interface
  - Comparable interface:
    - implemented by class being sorted
    - should be consistent with `equals`
  - Comparator interface:
    - implemented by class performing the sort
    - class performing sort != class being sorted

## Map Collections

- keys are unique
- values can be null

### Map Interfaces

- Map: Basic map operations
- SortedMap: Map with sorted keys

### Map Classes

- HashMap: Map with efficient general purpose
  - not synchronized
  - keys cannot be null, but values can be null+
  - better for non-threaded apps
- HashTable: Map that is synchronized
  - neither keys nor values can be null
- TreeMap: SortedMap implemented as a self-balancing tree. Supports Comparable and Comparator.

## Map Lambda

```java
// loop over key, value pairs
myMap.forEach((k, v) -> System.out.println(k +  " | " + v));

// change all values in map to uppercase
myMap.replaceAll((k, v) -> v.toUpperCase());
```
