## Inner Classes
- Inner class = nested class
- Four main cases

### 1. Member Inner Class
- Used to logically separate code in a class. Each group = 1 inner class.
- Ex: Robot class may contain inner classes: brain, arms, legs, power
- Can access all instance variables (even private ones)
- Usually accessed only by outer class, but can be accessed outside.
``` java
// inside outer class
Inner inside = new Inner();

// outside outer class (if inner class is public of course)
// Not very common
// An instance of Outer is needed
Outer outerInst = new Outer();
Outer.Inner outside = outerInst.new Inner();
```
- If needed by external class, usually the outer class will create the inner class instance and return it to the external class.

### 2. Static Inner Class
- Cannot access non-static instance variables
- It's an inner class that is not associated to instances of outer class
- It's just grouped with the outer class, but not dependent on it
- Common to be accessed by external classes
``` java
// assumes public. An instance of Outer is not needed.
Outer.Inner staticInst = new Outer.Inner();
```

### 3. Anonymous Inner Class
- Creates a class without a name
- Used to implement or override methods
- Can access instance variables and local variables (as long as ```final``` is used)
``` java
interface Phone {
  void show();
}

public static void main() {
  // anonymous class
  Phone p = new Phone() {
    public void show() {
      // provides implementation
      System.out.println("Implementation");
    }
  }
}
```

### 4. Local Inner Class (inside method)
- Class is inside a method
- Has access to instance variables (even private)
- Has access to local variables (inside method) as long as they use ```final```
- Cannot be accessed from outside of the method
- Can only be accessed inside the method
- Sometimes useful
