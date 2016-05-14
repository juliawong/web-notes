# Python

## Functional Programming 

* https://codesachin.wordpress.com/2016/04/03/a-practical-introduction-to-functional-programming-for-python-coders/
* https://maryrosecook.com/blog/post/a-practical-introduction-to-functional-programming

* Pure functions don't rely on state
  * You get the same output with the same set of inputs
  * Return a new instance
* Lambda operative helps create pure functions in Python
* We can pass the functions as arguments

``` python
>>> square_func = lambda x: x**2
>>> square_func(2)
4
>>> some_list = [(1, 3), (5, 2), (6, 1), (4, 6)]
>>> some_list.sort(key=lambda x: x[0]**2 - x[1]*3)
>>> some_list
[(1, 3), (4, 6), (5, 2), (6, 1)]
```

* Recursion is possible
  * Use tail-recursion in compiled languages for better optimisation

### Map, Reduce, Filter

* One liners
* Collection, operation and return value are always in the same place
* Not affected by when vars have to be defined like in a loop
* Building blocks to instantly understand what operation is occurring

* map
  * Calls a function over all elements in an array
  * Makes a new empty collection, inserts return value of function and returns new collection
  * e.g. square all elements

``` python
>>> map(lambda x: x**2, [1, 2, 3])
[1, 4, 9]
```

e.g. list of lengths

``` python
name_lengths = map(len, ["Mary", "Isla", "Sam"])
[4, 4, 3]
```


* filter
  * retains values from sequence that return true from function
  * e.g. retain all even numbers

``` python
>>> filter(lambda x: x % 2 == 0, [1,2,3,4,5,6])
[2, 4, 6]
```

* reduce
  * performs serial iteration over sequence, combines items
  * first arg is a function taking accumulator and current input
  * second arg is the sequence to reduce
  * third arg is the initial accumulator
  * e.g. sum all numbers, initial accumulator of 0

``` python
>>> reduce(lambda x, y: x + y, [1, 2, 3], 0)
6
```

* `x` is the accumulator
* `y` is the current item being iterated over
* result stored back in `x`
* If there is no initial accumulator, the first element is `x` and the second element is `y`


## Comprehensions

### Lists

* `[x**2 if x % 2 == 0 else x**3 for x in range(10)]` x if y else z
* Can nest inside each other `[[0 for x in range(10)] for y in range(10)]`

### Generator Expressions

* Don't require us to create a temporary list in memory
* Pass it the comprehension
* `sum(x**2 for x in range(20))`
* `set(word for word in vocab_list if word not in known_words)`
* `dict((grade, convert_to_letter(grade)) for grade in report_card)`

### Dict

* `{key: value for (key, value) in iterable}`
* e.g. initialise letter frequencies
* `{c: 0 for c in string.ascii_lowercase}`
* e.g. take 2 lists and create dictionary
* `{k: v**3 for (k, v) in zip(string.ascii_lowercase, range(26))}`
* `zip` returns an iterator of tuples, maintains order of input iterables
* Can have if else constructs e.g. omits cubes not divisible by 4
* `{x: x**3 for x in range(10) if x**3 % 4 == 0}`

### Set

* Set is an unordered collection of unique elements
* `{EXPRESSION FOR ELEMENT IN SEQUENCE}`
* Python 3 `{n**2 for n in range(10)}`
* `set(n**2 for n in range(10))`

