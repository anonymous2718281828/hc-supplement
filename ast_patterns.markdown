---
layout: default
title: AST Patterns
---
# Candidate Locations

In the following sub-page, we give a brief overview of the AST patterns that we match to identify candidate locations.

## LocalConst

The LocalConst pattern captures occurences of const-qualified variables in a local scope (e.g., within a function), that are directly intialized with a literal value.

For example, in the following snippet:

```cpp

void foo() {
    int bar = 10;

    const int baz = 20;

    return baz;
}
```

The variable `baz` matches this pattern, while `bar` does not as it is not const-qualified.

## GlobalConst

This pattern is similar to the LocalConst pattern. However, it captures variable declarations on a global scope and not only within functions.

For example:

```cpp
const float factor = 0.25f;

namespace Bar {
    const long MAGIC = 12345;    

    void foo() {
        ...
    }
}
```

Both `factor` and `MAGIC` would be matched by this AST pattern.

## ConstField

Matches all occurrences of const-qualified fields in a `class` or `struct`.

For example:
```cpp
struct Foo {
    const short A = 10;
    uint8_t B = 20;
}

class Bar {
    const double V = 0.5;
    short D = 5;
}
```

Matches the declaration of `A` in the struct `Foo` and `V` in the class `Bar`.

## TemplateLiteral

This AST pattern matches instantiations of template classes with numeric literals.

For example:
```cpp
template <int T>
class C {
    ...
}

C<12> Inst1;

void foo() {
    C<25> Inst2;
    ...
}

```

Matches both `Inst1` and `Inst2`.

## LiteralBinOp

This pattern matches all binary operations where one side is a literal value.
We exclude all occurrences with the literals `0` or `1` as we assume that these are commonly used to check for empty containers or as termination conditions for loops.

For example, in:

```cpp

void foo(int v) {

    if (v == 25) {
        ...
    }

    if (v > 12) {
        ...
    }

    do {
        ...
        --v;
    } while( v > 0);
}

```

This patterns matches both conditions of the `if` statements, but not the termination condition of the `do-while` loop.

