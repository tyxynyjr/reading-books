# Core Java - Fundamentals

## Collections

The data structures that you choose can make a big difference while solving
problems, and the collections library is that offered by Java to help with the
data structure challenges for serious programming. As is common with modern data
structure libraries, the Java collection library separates interfaces and
implementations.

Taking the interface of `Queue` for example, a minimal form of interface might
look like this:

```java
public interface Queue<E> // a simplified form of the interface in the standard library
{
    void add(E element);
    E remove();
    int size();
}
```

Java also offers abstract class that implements the routine methods in the
general interfaces, which makes it more suitable for the developer to extend.

### Iterators

The `Iterator` interface has four methods:

```java
public interface Iterator<E>
{
    E next();
    boolean hasNext();
    void remove();
    default void forEachRemaining(Consumer<? super E> action);
}
```

As of Java SE 8, you can call the `forEachRemaining` method with a lambda
expression that consumes an element.

### Linked Lists

Arrays and array lists suffer from a major drawback that removing an element
from the middle of an array is expensive since all array elements beyond the
removed one must be moved toward the beginning of the array. The same is true
for inserting elements in the middle. The class `LinkedList` is available in
Java to solve this issue.

### Array Lists
