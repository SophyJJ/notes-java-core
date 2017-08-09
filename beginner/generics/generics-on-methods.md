## Generics On Methods

- You can make generic methods
- The types are only visible in that method
-

```java
public class SortingExample {
    public static void main(String[] args) {
        Person person1 = new Person("person1", 89);
        Person person2 = new Person("person2", 65);
        Person person3 = new Person("person3", 100);

        List<Person> people  = new ArrayList<>();
        people.add(person1);
        people.add(person2);
        people.add(person3);

        final Person youngest = min(people, new Comparator() {
            public int compare(final Person left, Person right) {
                return Integer.compare(left.getAge(), right.getAge());
            }
        });

        System.out.println(youngest);

        List<Integer> nums = new ArrayList<>();
        nums.add(2);
        nums.add(1);
        nums.add(3);

        // Method reference introduced in Java 8
        final Integer minNumber = min(nums, Integer::compare);
        System.out.println(minNumber);
    }

    // input type HAS to be between access modifiers and return type
    // type only visible in this method
    public static <T> T min(List<T> values, Comparator<T> comparator) {
        if (values.isEmpty()) {
            throw new IllegalArgumentException("List is empty. Cannot find minimum");
        }

        T lowestElement = values.get(0);
        for (T element : values) {
            if (comparator.compare(element, lowestElement) < 0) {
                lowestElement = element;
            }
        }
        return lowestElement;
    }
}
```
