# Symbols

Differently from other atoms, symbols in Common Lisp are usually evaluated
to some objects other than itself.
That is to say, **symbols in Common Lisp act the role of function names,
macros, type names, variables, and so on, in other programming languages.**

## Symbol Names

A symbol is a sequence of characters.
This sequence of characters is called a **symbol name**, which is the identity
of the symbol.

Symbol names are case insensitive.
Hence, for example, `foo`, `fOO` and `Foo`, and so on, are the same symbol.
For another example, `pi`, `Pi`, `pI` and `PI` are the same symbold,
which is a built-in constant in Common Lisp, having the value
`3.1415926535897932385L0`.

Two symbols are the same if and only if their symbol names are same,
up to case difference.

In principle, any character can be used in symbol names.
For examples, `family-name`, `first-name`, `姓名` are all accepted as
symbol names.
* Because whitespaces and parentheses are delimiters of atoms, while symbols are
    also atoms, if a symbol name contains a whitespace or a parenthesis,
    these characters must be escaped.  That is, they should be written as `\ `,
    `\(` and `\)`, respectively.
    It follows that the backslash is also a special character.
    Hence, if a backslash is contained in a symbol name, the backslash should be
    written as `\\`.
    For example, `copyright\ \(C\)\ @2023\\` is a valid symbol name.
* If a sequence of characters can be interpreted as an atom other than a symbol,
    this sequence cannot be a symbol name.  For example, `123`, `#xFACE`, `1/2`,
    `1.5e-20` are judged to be numbers by Common Lisp reader, hence they cannot
    be symbol names.
    For another example, `"foo"` is a string in Common Lisp, hence it cannot be
    a symbol name.  Instead, `\"foo\"` is a valid symbold name.
* Since the semicolon (`;`) starts comments in Lisp, this character should be
    written as `\;` whenever it is contained in a symbol name.
* The following characters must be escaped in symbold names: `#`,
    the backquote (backtick) (<code>\`</code>), the single quote (`'`),
    the comma (`,`) and the colon (`:`).

In the above, we have shown those special characters and how they are escaped
in symbol names.  Alternatively, we can put the whole symbol name between a pair
of verticle bars, so that special characters need not be preceded by `\`.
For example, `|copyright (C) 2021; 2022; 2023 \n|` is a valid symbol name.
**It follows that `|` must be written as `\|` when it is contained
in a symbol name.**


In Lisp, symbols `+`, `-`, `*` and `/` are applied to name the four common
arithmetic operations: `+` for addition, `-` for subtraction,
`*` for multiplication, and `/` for division.
Their usage are as shown in the following examples:

| Arithmetic expression | Lisp codes | Remarks |
| --------------------- | ---------- | ------- |
| 3/10 + (-1/5) | `(+ 3/10 -1/5)` | Evaluates to `1/10` |
| 2 + 0xF | `(+ 2 #xF)` | Evaluates to `17` |
| 2 - 8 | `(- 2 8)` | Evaluates to `-6` |
| 3 * (1/3) | `(* 1 1/3)` | Evaluates to `1` |
| 2 / (-10) | `(/ 2 -10)` | Evaluates `-1/5` |
| (1 + 2)/4 | `(/ (+ 1 2) 4)` | Evaluates to `3/4` |

However, the above characters `+`, `-`, `*` and `/` in a symbol name have
nothing to do with arithmetic operations.  For example, `uid+pid` is a single
symbol name, not the addition of two variables `uid` and `pid`.
Similarly, `family-name` is a single symbol name, not the subtraction of
variables `family` and `name`.

In Lisp, there is a convention that every global variable has its symbol name
beginning and ending with asterisk (`*`), like `*var-1*` and `*no-proof*`,
as examples.

The built-in global variable `*read-base*` is the current number base (radix),
which defaults to `10`.
If a symbol name is interpreted to be a number in the current number base,
then it is not a valid symbol name, but a number.
For example, when `*read-base*` is `16` or greater, `face` is not a symbol name
but a number;  when `*read-base*` is less than `16`, `face` is a symbol name.

Conventionally, the name of a constant is often written with a leading `+`
and a trailing `+`.
But built-in constants in Lisp do not follow this convention.  For example,
```
  pi
  most-positive-fixnum
  least-negative-short-float
```

A symbol is called **self-evaluating** if it has itself as its value.
A symbol in the `KEYWORD` package is self-evaluating.
A symbol beginning with the colon (the character `:`) is a keyword symbol.
Hence the character `:` is called the **package prefix**.[^1]
Each keyword symbol is evaluated to itself.

## References

[^1]: David B. Lamkins, [*Successful Lisp*](http://dept-info.labri.fr/~strandh/Teaching/MTP/Common/David-Lamkins/cover.html).
