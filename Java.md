# Rounding

* `System.out.printf("%.6f\n", number);`
* `.6` means to 6 decimal places
* `%f` represents a float

# Set

* Fail-fast iterators, if set modified during iteration, `ConcurrentModificationException` thrown
* Implemented on top of map
  * Returns true if new key
  * Return false if existing key
  * `PRESENT` is a `new Object()`
  * Maintains uniqueness
  ``` Java
    public boolean add(E e) {
      return map.put(e, PRESENT)==null;
    }
  ```

## TreeSet
* Elements sorted using red-black tree
* Can pass a Comparator to order, priority over natural ordering
* Does not allow for null objects
* O(log n) for add, remove, contains
* Additional functions pollFirst, pollLast, first, last, ceiling, lower, etc.
* Not thread safe
* Use when sorting is desirable and read/write operations are frequent
* Has greater locality than hashset

## HashSet
* Use hash of element to store
* O(1) for add, remove, contains
* Not thread safe

# ArrayList And Vector

* Vector is thread safe, slower
* ArrayList increases capacity by 50%
* Vector doubles capacity
* Can set size of the vector using `setSize`
* Vector uses enumeration and iterator
* ArrayList uses only iterator

# Iterator and Enumeration

* Iterator
  * `hasNext`, `next`, `remove`
  * Used in collections framework
  * Can remove elements from collection during iteration
* Enumeration
  * `hasMoreElements`, `nextElement`
  * Generates one element at a time
  * Pass through a collection of unknown size
  * Traverse once per creation

# Comparable and Comparator

* Interfaces

## Comparable

* Impose natural ordering of class implementing
* Comparison of two objects is the comparison of ASCII values
* Takes another object to comapre with `this`, `compareTo(Object o)`
* Modify class to implement
* Can be used in `Collections.sort()`, `compareTo` used to sort
* Can be used as keys in sorted collections

## Comparator

* Impose ordering on collection of objects
* Function
* Control over the sort order, e.g. different parameters in class
* Can create many sort sequences
* Takes 2 objects `compare (Object o1, Object o2)`
* Requires additional class, ideal if class can't be modified
