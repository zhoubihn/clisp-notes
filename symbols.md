
    Differently from other atoms, symbols in Common Lisp are usually evaluated
    to some objects other than itself.
    That is to say, **symbols in Common Lisp act the role of function names,
    macros, type names, variables, and so on, in other programming languages.**

    For details of symbols in Common Lisp, we refer to [symbols.md](symbols.md).

    A symbol is a sequence of characters.
    This sequence of characters is called a **symbol name**.
    Symbol names are case insensitive.
    Hence, for example, `foo`, `fOO` and `Foo`, and so on, are the same symbol.
    For another example, `pi`, `Pi`, `pI` and `PI` are the same symbold,
    which is a built-in constant in Common Lisp, having the value
    `3.1415926535897932385L0`.

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

    A symbol beginning with the colon (the character `:`) is a keyword symbol.
    Hence the character `:` is called the **package prefix**.
    Each keyword symbol is evaluated to itself.
