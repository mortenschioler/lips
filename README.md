Lips is a minimal dialect of Lisp that is meant for conceptual and illustrative
purposes, and not for use as a practical programming language. That being said,
it can be used for simple general purposes.

# Specification

## Data types

### Scalars

#### Number

The only supported numeric type is the integer. Literals are written in decimal
format only, and the size of the data type is undefined, meaning the implementor
is free to use whatever number bytes (octets) that is convenient. Negative numbers
must be supported.

#### Symbol

Symbols are string-like scalars that may consist of only a-z, A-Z and the dash 
character (`-`).


#### `nil`

The symbol `nil` always evaluates to the null pointer. `nil` is falsy.

#### Booleans (`true` and `false`)

The symbols `true` and `false` resolve to their respsective logical scalar values.
`false` is falsy. `true` is, like every other value except `nil` or `false`, truthy.

#### Function

A function is a scalar with no literal representation that can be executed. Functions
have lexical scope and support closures.


### Aggregate data types

#### List

Lists are a primitive type and are written in the traditional literal notation of Lisp:
  (1 2 3)


## Built-in functions

### `+`

Adds its argument together. When given no arguments, returns 0.

### `-`

Subtracts the rest of its arguments from the first. If given only one argument, return
the negation instead. When given no arguments, return 0.

### `*`

Returns the produc of its arguments, or 1 if given no arguments.

### `/`

Returns 1 when given no arguments, the argument itself when given exactly one, and the 
result of successive division of first argument by the rest when given several arguments.

### `<`

Predicate whether its arguments are monotonically strictly increasing.

### `>`

Predicate whether its arguments arew monotonically strictly decreasing.

## Special forms

### `(if condition then else)`

S-expressions starting with `if` are evaluated differently. First, the condition is evaluated.
If `condition` is truthy, `else` is ignored (not evaluated) and the value of the `if` expression becomes
the evaluation of `then`, and vice versa if `condition` is falsy..

### `(def symbol expression)`

Evaluates `expression` in the current global environment, and updates the global environment
by associating `symbol` with the resulting value.

### `(lambda (arguments) expression)`

Return a function that represents the delayed evaluation of the expression within its lexical scope
of origin, with the arguments in the argument list overriding that surrounding lexical scope with the
arguments that are passed upon evaluation.
