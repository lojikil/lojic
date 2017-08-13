# Overview

This repository is meant to keep record of the C dialect I tend to use in my projects, as well as
a tool for parsing the same. It is a mix of syntactic styles & semantic restrictions. The goal is
that every valid LojiC program is a valid C program, but not the reverse. You can read this as that
LojiC is a subset of C proper.

# Influences

LojiC is the style of C I've been using over a few years, influenced by:

- Cyclone
- Single-Assignment C
- Clight
- MISRA C

Recent languages like Low\*, &c. are also within my wheelhouse.

# Ideas

Below are some rough rules that make up the coding style I've been trying to adhere to. Eventually,
it would be nice to compare the below to the C standard, and clean up any "undefined behaviour" (UB),
and start to formalize the ideas a bit, such that compiling from higher-level languages to LojiC will
be well understood. This would include tooling, and model extraction from those HLLs.

## Semantics

- assignments are statements (and thus return a "meaningless" value)
- procedures vs functions (the return of the former is "meaningless")
- only use `++` & `--` in `for` loops
- use `+=` & `-=` elsewhere
- no direct pointer arithmetic
- instead use array indicies
- fat pointers & never nil
- no assignment in `if` conditions
- avoid non-tail recursion
- rewrite tail recursion to a loop, such as `while`
- avoid varargs, and prefer typed lists
- avoid `void *` and the like
- `const` and `restrict` pointers wherever possible
- functions not used outside their unit should be declared `static`
- avoid global variables, even `static` ones
- use enums wherever possible for magic numbers, unless they are one-offs (then use `#define`)

## Syntax

- all blocks use `{}`, no exceptions
- `{` on the same line as the block opener, `}` on its own line
- the only exception is if-else chains
- spaces, not tabs
- no names in forward declarations
- typedef & name structs
- do not use `name_t` ala POSIX
- capitalize structure names
- return type on its own line in function definitions
- use of `void` parameter lists when no values are needed
- no space between casts `(AST *)hmalloc(sizeof(AST))`
- use `sizeof(foo)` not `sizeof foo`
- only use `/* ... */` for comments, `// ...` is for killing code
- avoid macros, and esp. avoid macros with large chunks of code in them
- variables should be declared at the top of their scope wherever possible
- always indent blocks, including switch statements
- return early on failure
- prefer customized headers to `#ifdef` blocks, and APIs abstract enough to support that

# Related

- look into these [clang analyzers](https://github.com/sinelaw/elfs-clang-plugins/)
