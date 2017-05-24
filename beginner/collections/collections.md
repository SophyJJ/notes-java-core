# Collections

## What's problem with Arrays?
- not friendly to println
- arrays don't resize. Can't add new items. You need to write your own helper.
- very low level. You need to write lots of helpers
- can't specify constraints on elements, like duplicates, etc

## Java Collections Framework

- Java collections framework comes with the JDK. They implement data structures
- data structures are diverse. some provide ordering, uniqueness, pairs, etc
- they are complex. No need to rewrite your own.
- interfaces define behavior
- implementation define performance characteristics
- always use interface references variables so you can easily switch between implementations with polymorphism
- implementations are good for different things and have different performance in others
- use final iterator when removing from collection while looping through a collection

## Inheritance

- Collection (INT) -extends-> List (INT) -implements-> `ArrayList`, `LinkedList`
                   -extends-> Set (INT) -implements-> `HashSet`
                                        -extends-> SortedSet (INT) -implements-> `TreeSet`
                   -extends-> Queue (INT) -implements-> `PriorityQueue`
                                          -extends-> Deque (INT) -implements-> `LinkedList`, `ArrayDeque`
                   -extends-> Map (INT) -> `HashMap`
                                        -extends-> SortedMap (INT) -implements-> `TreeMap`

## How to pick interface?

- are elements key pairs?:
  - if yes:
    - is the order important?
      - if yes: USE a `SortedMap`
      - if no: USe a `Map`
  - if no:
    - are elements unique?
      - if yes:
        - is the order important?
          - if yes: USE a `SortedSet`
          - if no: USE a `Set`
      - if no:
        - first in, first out?
          - if yes: USE a `Queue` or USE a `Deque`
          - if no:
            - last in, first out?
              - if yes: USE a `Deque`
              - if no: USE a `List`
