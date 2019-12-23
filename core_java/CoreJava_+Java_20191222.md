# Core Java - Fundamentals

## Inheritance

### Object

A hash code is an integer that is derived from an object. The algorithm for
`String` to compute the hash code is as following, which is defined in the
`Object` class:

```java
int hash = 0;
for (int i = 0; i < length(); i++)
    hash = 31 * hash + charAt(i);
```

For strings, the hash codes are derived from their contents, for objects like
`StringBuilder` it derives the hash code from the object’s memory address

## Collections

The data structures that you choose can make a big difference while solving
problems, and the collections library is that offered by Java to help with the
data structure challenges for serious programming. As is common with modern data
structure libraries, the Java collection library separates interfaces and
implementations.

* A set is a collection that lets you quickly find an existing element

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

### Lists, Sets and Queues

Arrays and array lists suffer from a major drawback that removing or inserting
an element from or in the middle of an array is expensive since all array
elements beyond the removed one must be moved toward the beginning or ending of
the array. The class `LinkedList` is available in Java to solve this issue.

An `ArrayList` encapsulates a dynamically reallocated array of objects.

Looking for a particular element if the position is not remembered can be time
consuming if the collection contains many elements, because all elements should
be visited until a match is found. `hash table` is a well-known data structure
for finding objects quickly. The simplest data structure implemented with hash
table is the `set` type. A hash code is somehow derived from the instance fields
of an object, preferably in such a way that objects with different data yield
different codes.

A tree set is a sorted collection. The sorting is accomplished by a tree data
structure. And the current implementation uses a `red-black tree`.

A queue lets you efficiently add elements at the tail and remove elements from
the head. A double-ended queue, or deque, lets you efficiently add or remove
elements at the head and tail.

A priority queue retrieves elements in sorted order after they were inserted in
arbitrary order. The priority queue makes use of an elegant and efficient data
structure called a `heap`. A heap is a self-organizing binary tree in which the
add and remove operations cause the smallest element to gravitate to the root,
without wasting time on sorting all elements. A typical use for a priority queue
is job scheduling.

### Maps

The map data structure serves that purpose of looking up an element in key / value pairs.

* `HashMap`: hashes the keys
* `Treemap`: uses an ordering on the keys to organize them in a search tree

The easiest way of iterating over the keys and values of a map is the `forEach`
method. Removing a key in the key set view will remove the key and its
associated value from the map. However, adding an element to the key set or
entry set view is not possible.

A `WeakHashMap` cooperates with the garbage collector to remove key/value pairs
when the only reference to the key is the one from the hash table entry.

`EnumSet` and `EnumMap`