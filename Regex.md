# Regex

## Lazy and Greedy matching

Greedy matching will attempt to consume as many characters as possible
e.g. `<.+>` will match all of `<b>Hello, World!</b>` instead of just `<b>`

Lazy matching repeat as few times as possible
e.g. `<.+?>` will just match `<b>` from `<b>Hello, World!</b>`

These are lazy quantifiers:
* `*?`
* `+?`
* `??`
* `{m,n}?`

## Tools 
* https://regex101.com/ - explains, highlights, lists matches
* https://www.debuggex.com/ - visualiser
