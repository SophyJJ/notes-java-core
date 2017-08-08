## Implement Generic Type


```java

// Class Person
public final class Person {
    private final String name;
    private final int age;
    public Person(String name, int age) {
        Objects.requireNonNull(name);
        this.name = name;
        this.age = age;
    }
    // getters and setters
}


// main method
public static void main (String[] args) {
    Person person1 = new Person("name1", 34);
    Person person2 = new Person("name2", 30);

    List<Person> people = new ArrayList<>();
    people.add(person1);
    people.add(person2);

    // sort the list based on age
    Collections.sort(people, new AgeComparator());

    // print the sorted list
    System.out.println(people);

    // reverse any comparator
    Collections.sort(people, new ReverseComparator<Person>(new AgeComparator()));
}

// Age comparator class
public class AgeComparator implements Comparator<Person> {
    public int compare(final Person left, Person right) {
        return Integer.compare(left.getAge(), right.getAge());
    }
}

// Generic comparator reserval
public class ReverseComparator<T> implements Comparator<T> {
    private final Comparator<T> delegateComparator;

    public ReserverComparator(final Comparator<T> delegateComparator) {
        this.delegateComparator = delegateComparator;
    }

    public int compare(final Person left, Person right) {
        return -1 * delegateComparator.compare(left, right);
    }
}

```
