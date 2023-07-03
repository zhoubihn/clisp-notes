# Key Points in Common Lisp

## Syntax and Semantics of Common Lisp

### S-expressions

The term S-expression was invented for the programming language Lisp.
It has become an important concept in computer science.
An **S-expression** is recursively defined as either
* an atom, or
* an expression of the form `(x y)`  where `x` and `y` are S-expressions
  separated by a whitespace.

Atoms in Lisp will be explained in the subsection [Atoms](#Atoms) below.

In Lisp, all programs and data can be represented by S-expressions.
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
This can be illustrated as a binary tree as follows, where `o` represents
a node in the tree:
```
    o
   / \
  *   o
     / \
    o   3
   / \
  +   o
     / \
    1   2
```

In Common Lisp, an S-expression can be referred to by
a [**datum label**](datum-label.md).
By virtue of datum labels, an S-expression could have a structure of
cyclic graph, not simply a binary tree.

### Atoms

An *atom* in Lisp is an expression (a form) that is not built of
other independent Lisp expressions (forms).

The following objects are atoms in Lisp:
* a number, including
    * integers such as -2, -1, 0, 1, 2, and so on;
    * fractions such as
    * float numbers such as 1.0, 
* a string,
* a symbol.

Atoms are separated by whitespace or parentheses.


### Lists


### Forms
