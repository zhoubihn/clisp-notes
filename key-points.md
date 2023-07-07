# Key Points in Common Lisp

## Syntax and Semantics of Common Lisp

### S-expressions and Lists

The term S-expression was invented for the programming language Lisp,
widely accepted as an important concept in computer science.
An **S-expression** is recursively defined as either
* an atom, or
* an expression of the form `(x y)`  where `x` and `y` are S-expressions
  separated by a whitespace.

Atoms in Common Lisp will be explained in the subsection [Atoms](#Atoms) below.

In Common Lisp, all source codes and data can be represented by S-expressions.
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
In Common Lisp, there exists a special S-expression `(x y)` with `x` and `y`
being nothing.  Such an S-expression is denoted by `()`, and officially denoted
by `NIL`.

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

**However, in some Common Lisp implementations, a list with more than two
members are not identified with a nested ordered pairs as shown in the above.**
For example, in [GNU CLISP](http://clisp.org)-2.49.93+, the list
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
by whitespace of parentheses.  For example, the following expressions are
identical in Common Lisp: (1) the list
```
  (x1 x2 (y1 y2) x3)
```
in one line;  and (2) the list
```
  (x1
      x2
      (y1 y2)
      x3)
```
in four lines with indents;  and (3) the list
```
  (x1 x2(y1 y2)x3)
```
with some whitespaces omitted.
For the reason of readability, the last form `(x1 x2(y1 y2)x3)` is not
recommended.


### Atoms

An *atom* in Common Lisp is an expression (a form) that is not built of
other independent Common Lisp expressions (forms).
The precise meaning of this statement is unclear, in fact.
Therefore, we should list atoms in Common Lisp one by one.

1. In Common Lisp, `NIL` is an atom.  It is evaluated as `NIL`.

2.  In Common Lisp, an literal integer is an atom, evaluated to itself.

    A **literal decimal number** is an expression consisting of digits `0` to
    `9` only, sometimes leaded by a single character `+` or `-`.  For examples,
    `-11`, `-10`, `- 9`, ..., `- 1`, `0`, `1`, `2`, ... are all literal decimal integers.

    A negative literal decimal integer must be preceded by the sign `-`.
    A positive literal decimal integer can be preceded by the sign `+`,
    but it is not necessary.
    For example, `+256`, `+00256` and `256` are both evaluated to `256`.

    In a literal decimal integer, leading zeros are allowed and omitted
    during evaluation.
    Hence, for example, `00000000256` and `-000000256` are evaluated to `256`
    and `-256`, respectively.

    In Common Lisp, `+0` and `-0` are also integers, and they are both evaluated
    to `0`.

    In List, a literal hexadecimal number is written in the form of `#x...`,
    where `...` is an expression consisting of hexadecimal digits `0` to `F`.
    **Hexadecimal digits `A` to `F` are case insensitive.**
    A positive hexadecimal integer could have a positive sign `+` immediately
    after `#x`, but it is not necessary.
    A negative hexadecimal integer must have its negative sign `-` immediately
    after `#x`.
    For examples, `#x+10AF`, `#x10AF`, `#x10aF`, `#x0010AF`, and so on, are all
    evaluated to `4271`, and `#x-10AF` is evaluated to `-4271`.
    Similarly to literal decimal integers, `#x+0`, `#x+000`, `#x-0`, `#x-000`,
    `#x0`, `#x00000`, and so on, are all evaluated to `0`.

    Similarly, literal binary integers are written in the form of `#b...`,
    with `...` consisting of binary digits `0` and `1`, which might be preceded
    by a single sign `+` or `-`;
    literal octal integers are written in the form of `#o...`,
    with `...` consisting of digits `0` to `7`, which might be preceded by
    a sigle sign `+` or `-`.

    **The prefix `#b` can be written as `#B`, and similarly, `#o` as `#O`, and
    `#x` as `#X`.**

    In Common Lisp, the radix (base) of a number can be any integer `n` from `2`
    to `36`.  An integer in radix `n` is written in the form of `#nr...` or
    `#nR...`, with `...` some digits from `0` to `9`, together with necessary
    digits from `A` to `Z` (or `a` to `z`).  For example, `#36r-1ZY` is a valid
    integer in radix 36, which is evaluated to `-2590`.

    According to the [Common Lisp HyperSpec (CLHS)](http://www.lispworks.com/documentation/lw50/CLHS/Front/Contents.htm),
    there is no limit on the magnitude of an integer in Common Lisp.

3. In Common Lisp, each fraction is an atom.

    A fraction in Common Lisp can be written in the form of `m/n`, where `m`
    and `n` are some integers, and `n` is a positive integer.

    Usually, both `m` and `n` are literal decimal integers, and `m/n`
    is evaluated to the irreducible fraction `a/b` equal to `m/n`.
    That is, `a` and `b > 0` are coprime integers satisfying `m * b = n * a`.
    For examples, `5/10` is evaluated to `1/2` and `-5/10` is evalutated to
    `-1/2`.

    For a fraction in Common Lisp, both its numerator and denominator can be
    simultaneously binary integers, or simultaneously octal integers,
    or simultaneously hexadecimal integers.
    In these cases, the radix (base) sign is written as the prefix of
    the fraction.  For example, `#b10/10000`, `#o1/10` and `#x2/10` are
    all valid fractions, all evaluated to `1/8`.
    For another example, `#b-10/10000`, `#o-1/10` and `#x-2/10`
    are all valid fractions, all evaluated to `-1/8`.

4. In Common Lisp, each floating-point number is an atom.

    **Floating-point numbers in Common Lisp can be expressed in radix 10 only.**
    There is no floating-point numbers in radix other than 10
    built in Common Lisp.

    The basic format of a **floating-point number** in Common Lisp is:
    an optional sign, followed by a nonempty sequence of decimal digits
    with an embedded decimal point.
    The decimal point can be at any position in the sequence of digits.
    For example, floating-point numbers `1.` and `1.0000` are both evaluated to
    `1`, while `.1`, `.10`, `0.10` and `0.1` are all evaluated to `0.1`.

    Floating-point numbers in Common Lisp can be written in the following form:
    an integer or a floating-point number in the basic format
    immediate followed by an exponent marker.
    An **exponent marker** consists of a single letter among `e`, `s`, `f`, `d`
    and `l`, immediately followed by a signed integer `n` say, which consists of
    an optional sign and a nonempty sequence of digits from `0` to `9`.
    The integer `n` is interpreted as the exponential to the power of 10.
    For example, `2e0`, `2e+0` and `2.e-0` are all evaluated to `2.0`, and
    `123e-5` is evaluated to `0.00123`.

    For the exponent marker,
    * the letter `s` indicates that the floating-point number is
        a short floating-point number, and
    * the letter `f` indicates that the floating-point number is
        a single floating-point number, and
    * the letter `d` indicates that the floating-point number is
        a double floating-point number, and
    * the letter `l` indicates that the floating-point number is
        a long floating-point number, and
    * the letter `e` is the default floating-point number:
        single floating-point number.

    Letters `e`, `s`, `f`, `d` and `l` are case insensitive.
    Therefore, `12.3f6` and `12.3F6` are the same.

5. In Common Lisp, each complex number is an atom.

    In Common Lisp, a complex number is written as `#c` (or `#C`) followed by
    a list of two numbers.
    Each of these two numbers can be an integer, a fraction
    or a floating-point number.
    * If the member in the list is an integer or a fraction, it can be
        written in any radix from `2` to `36`.
    * There can be whitespaces between `#c` (or `#C`) and the list of
        two numbers.

    For example, `#c(0 1)` is the imaginary unit, whose equare equals `-1`.
    For another example, #c(1 0)` is evaluated to `1`.
    Finally, there are the examples `#c(#b10 2.0e-9)` and
    `#c(1/2 5)`.

6. In Common Lisp, characters are atoms.

    Here character means a single code in certain a character encoding system
    (ASCII, UTF-9 or UTF-16, for example).
    Different encoding systems assign different numbers to certain a character.
    Thus characters are distinct from integers.
    The Common Lisp standard did not mandate a particular encoding system.
    This leaves a freedom for Common Lisp implementations.

    The read syntax for a character is `#\` immediately followed by
    the character to be read.  For example, `#\a` for letter `a` and
    `#\魚` for a Chinese character (meaning fish).
    Note that both `#\ ` and `#\Space` result in the space character.

7. In Common Lisp, each string is an atom.

    A string in Common Lisp is a sequence of characters, such as
    `"Hello, world!"` and "四方上下曰宇，古往今來曰宙。".
    The format of strings in Common Lisp is putting the desired sequence of
    characters in a pair of double quote mark (`"`).
    In other words, a double quote mark is the beginning of a string,
    which ends at the next quote mark.
    Hence the quote mark is a special character in Common Lisp.
    If there exists a character in the string being the quote mark,
    it must be written as `\"`.
    It follows that the backslash (`\`) is also a special character
    (called the **escape character**).
    When this escape character appears in a string, it must be written as
    `\\` in the Common Lisp code.

    Here are some examples:

    | Literal form    | What represented | Remarks |
    | --------------- | ---------------- | ------- |
    | `"foo bar"` | foo bar | Whitespaces in strings: not delimiters for atoms |
    | `"foo (bar)"`   | foo (bar) | Parentheses in strings: not delimiters for atoms |
    | `"foo\\bar"`    | foo\bar          | How the backslash is represented |
    | `"\"foo\" bar"` | "foo" bar        | How the quote mark is represented |

8. In Common Lisp, each symbol is an atom.

In Common Lisp, atoms are separated by whitespace and/or parentheses,
but whitespaces and parentheses in strings are exception.
Note that atoms in a pair of parentheses are members of a list.  For example,
`(f(x y z)g)` is the same as `(f (x y z) g)`, being the list with members
`f`, `(x y z)` and `g`, among which `(x y z)` is a list with members `x`, `y`
and `z`.
This rule is the same as how members in a list are separated.
See, subsection [S-expressions and Lists](#S-expressions-and-Lists).

**Since whitespaces make sense in Common Lisp, there should be no whitespaces
before or after the positive sign, the positive/negative sign,
the radix signes `#b`, `#o`, `#x` and `#nr` (with `n` an integer from 2 to 36),
and the slash in a fraction.**
For example, for negative numbers `-5`, `#x-5`, `-1/2`, `-1.2`, and so on,
there should not be whitespaces before or after the negative sign `-`,
and no whitespaces after `#x`, either.
Hence `- 5`, `#x- 5`, `#x -5`, `#x - 5`, `- 1/2`, `-1 / 2`, `-1 /2`, `- 1/ 2`,
`- 1.2`, and so on, are all invalid expressions to be numbers.
It is similarly the case for the positive sign `+`.


The following objects are atoms in Common Lisp:
* a number, including
    * integers such as -2, -1, 0, 1, 2, and so on;
    * fractions such as
    * floating-point numbers such as 1.0, 
* a string,
* a symbol.

Atoms are separated by whitespace or parentheses.


### Lists


### Forms
