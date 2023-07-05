# Key Points in Common Lisp

## Syntax and Semantics of Common Lisp

### S-expressions and Lists

The term S-expression was invented for the programming language Lisp,
widely accepted as an important concept in computer science.
An **S-expression** is recursively defined as either
* an atom, or
* an expression of the form `(x y)`  where `x` and `y` are S-expressions
  separated by a whitespace.

Atoms in Lisp will be explained in the subsection [Atoms](#Atoms) below.

In Lisp, all source codes and data can be represented by S-expressions.
For example, the arithmatic expression `1 + 2` can be represented by
the S-expression
```
  (+ (1 2))
```
while a more complicated expression such as `(1 + 2) * 3` can be represented by
the S-expression
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

An S-expression `(x y)` is an ordered pair `(x, y)` in nature.
In Lisp, there exists a special S-expression `(x y)` with `x` and `y` being
nothing.  Such an S-expression is denoted by `()`, and officially denoted by
`NIL`.

An S-expression `(x y)` can be called a **list** with two members.
In some literature, a list with more than 2 members is defined in terms of
S-expressions (ordered pairs).  For example, a list `(x y z)` with three members
`x`, `y` and `z` is defined to be a nested S-expressions (ordered pair) as
```
  (x (y (z NIL)))
```
and so on.  It seems that a list is also called an S-expression with more than
two memebers, hence the terms ``list'' and ``S-expression'' can be used
interchangeably.

**However, in some Common Lisp implementation, a list with more than two members
are not identified with a nested ordered pairs as shown in the above.**
For example, in [GNU CLISP](http://clisp.org) 2.49.93+, the list
```
  (+ 1 (* 2 3))
```
is evaluated to be `7`, but the nested lists (ordered pairs)
```
  (+ (1 ((* 2 3) NIL)))
```
and
```
  (+ (1 ((* (2 (3 NIL))) NIL)))
```
cannot be evaluated.

Therefore, we should think that, in Common Lisp, a list with multiple members
is just a sequence of its members, not identical to some nested ordered pairs
if it contains more than two members.
Accordingly, lists in Common Lisp should be defined as follows.
Assume that `n` is a positive integer, then
* there exists a unique list with no members, which is denoted by `()` or `NIL`;
* a list with `n` members is a sequence `(x1 x2 ... xn)`, with `x1`, `x2`, ...,
  `xn` some atoms or lists in Common Lisp.

If a list in Common Lisp has members more than one, these members are separated
by whitespace of paratheses.  For example, the following expressions are
identical in Common Lisp:
```
  (x1 x2 (y1 y2) x3)
  (x1
      x2
      (y1 y2)
      x3)
  (x1 x2(y1 y2)x3)
```
For the reason of readability, the form `(x1 x2(y1 y2)x3)` is not recommended.


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
