# Key Points in Common Lisp

## Syntax and Semantics of Common Lisp

### S-expressions

The term S-expression was invented for the programming language Lisp.
It has become an important concept in computer science.
An S-expression is recursively defined as either
* an atom, or
* an expression of the form `(x y)`  where `x` and `y` are S-expressions
  separated by a whitespace.

Both a program and a data can be represented by certain an S-expression.
For example, the arithmatic expression `1 + 2` can be represented by
the S-expression
```
  (+ (1 2))
```
while a more complicated expression such as `(1 + 2) * 3` can be represented by
the S-expresion
```
  (* ((+ (1 2)) 3))
```
