[CSS Diner](http://flukeout.github.io/)

* Descendant selector
  * `A B`
  * selects element inside another
  * e.g. `#fancy span` selects `span` elements that are descendants of elements with id `fancy`
* Class selector
  * `A.className`
  * Select item with class
  * e.g. `#big.wide` selects all elements with id `big` with class `wide`
* Comma combinator
  * `A, B`
  * Select all listed elements
  * e.g. `a, p, div` will select all of these elements
* Universal Selector
  * `*`
  * Select ALL the things!
  * e.g. `p *` selects all elements inside `p`
* Adjacent sibling selector
  * `A + B`
  * Selects all B elements that directly follow A
  * Same level in hierarchy i.e. siblings
  * e.g. `div + a` selects every `a` element that follows a `div`
* General sibling selector
  * `A~B`
  * Select all siblings of an element that follow it, like adjacent but takes all
  * e.g. `bento~pickle` selects all pickles to the right of the bento
* Child selector
  * `A > B`
  * Selct direct children of an element
  * Elements nested deeper than children are called descendant elements
  * e.g. `plate > apple` selects all apples that are direct children of plate
* Pseudo-selectors
  * First child
    * `:first-child`
    * first child element
    * e.g. `div p:first-child` selects all first child `p` elements in `div`
  * Only child
    * `:only-child`
    * Select elementthat is the only element inside of another
    * e.g. `ul li:only-child` selects the only `li` element in `ul`
  * Last-child
    * `:last-child`
    * Select last element inside of another element
    * e.g. `ul li:last-child` selects the last `li` element in `ul`
  * Nth child
    * `:nth-child(A)`
    * Selects nth child element
    * `div p:nth-child(2)` selects second `p` in every `div`
* Nth-last-child
  * `:nth-last-child(A)`
  * Selects nth element starting from bottom of parent
  * e.g. `:nth-last-child(2)` selects all second-to-last child elements
* First of Type
  * `:first-of-type`
  * Selects first element of that type within element
  * e.g. `span:first-of-type` selects first `span` in any element
* Nth of type
  * `:nth-of-type(A)`
  * Selects specific element
  * Can pass in `even` or `odd`
  * Or use `2n`
  * e.g. `.example:nth-of-type(odd)` selects all odd instances of the example class
  * `:nth-of-type(An+B)`
  * Can have formula
  * Determine start and step
  * e.g. `span:nth-of-type(6n+2)` selects every 6th instance of a `span`, starting from (and including) the second instance
* Only of type
  * `:only-of-type`
  * Selects only element of its type within element
  * e.g. `p span:only-of-type` selects a `span` within any `p` if it is the only `span` in there.
* Last of type
  * `:last-of-type`
  * Selects last element of a specific type
  * e.g. `div:last-of-type` selects last `div` in every element
* Empty
  * `:empty`
  * Select elements that don't have children
  * e.g. `div:empty` selects all empty `div` elements
* Negation Pseudo-class
  * `:not(X)`
  * Selects all elements that don't match selector `X`
  * e.g. `:not(.big, .medium)` selects all elements that don't have class big or medium


