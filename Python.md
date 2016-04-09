# Python

## Functional Programming 
https://codesachin.wordpress.com/2016/04/03/a-practical-introduction-to-functional-programming-for-python-coders/

* Pure functions don't rely on state
* * You get the same output with the same set of inputs
* * Return a new instance
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
* * Use tail-recursion in compiled languages for better optimisation

### Map, Reduce, Filter

* map
* * Calls a function over all elements in an array
* * e.g. square all elements

``` python
>>> map(lambda x: x**2, [1, 2, 3])
[1, 4, 9]
```


* filter
* * retains values from sequence that return true from function
* * e.g. retain all even numbers

``` python
>>> filter(lambda x: x % 2 == 0, [1,2,3,4,5,6])
[2, 4, 6]
```

* reduce
* * performs serial iteration over sequence
* * first arg is a function taking accumulator and current input
* * second arg is the sequence to reduce
* * third arg is the initial accumulator
* * e.g. sum all numbers, initial accumulator of 0

``` python
>>> reduce(lambda x, y: x + y, [1, 2, 3], 0)
6
```
