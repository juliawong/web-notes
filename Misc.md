Other notes which I am yet to find a category for

# Bus Factor
* Measurement of the concentration of information in individual team members
* How many people in the team can we unexpectedly lose due to being hit by a bus, before the project collapses?
* Avoid this by closer collaboration e.g. stand ups, pair program, code reviews, presentations

# Bloom Filters

TODO


# Maths

## Arithmetic series

![arithmetic series](http://i.imgur.com/aFOthab.gif)

* Used to find the sum of numbers starting from 1 to n
* i.e. 1 + 2 + 3 + ... + n

![arithmetic series](http://i.imgur.com/hS74rAt.gif)

* take the number of terms being added
* multiply by sum of first and last number
* divide by two
* this formula takes the start term and end term

### Sum factors

e.g. find the sum of all multiples of 3 in k, where k is an integer

* n = k / 3
  * This is the total number of multiples we have (assume this is truncated)
* use the first arithmetic formula
* multiply by 3

e.g. k = 14

* n = 14 / 3 = 4 (truncated)
* use formula
* ![formula with n=4](http://i.imgur.com/wlau9Pz.gif)
* multiply by 3 to get sum of multiples of 3 in 10
* 30

What's happening

* (1x3) + (2x3) + (3x3) + (4x3) = (1 + 2 + 3 + 4) x 3 = 10 x 3 = 30
* We use the arithmetic sum to get the sum of the first numbers
* We then multiply this by the multiple to get the answer

