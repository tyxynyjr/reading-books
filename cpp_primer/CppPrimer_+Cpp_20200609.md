# C++ Primer

## Variables and Basic Types

### Primitive Built-in Types

* Types determine the meaning of the data and the supported operations.

A literal is a value which is self-evident. And the form and value of a literal
determine its type.

* Integer literal: decimal (20), octal (024) and hexadecimal (0x14 or 0X14)
    + Note: the minus sign in integral literal e.g. -24 is not part of the
      literal, instead, it is an operator
* Floating-point literal: with either decimal point (3.1415, 0., 0.0 or .1) or
  scientific notation (3.1415e0 or 3.1415E0)
* Character literal
* String literal
    + Note: two string literals separated by spaces, tabs and newlines are
      concatenated into a single string literal
* Escape sequence: characters are non-printable (newline, tab etc.) or with
  special meaning (single / double quote, question mark etc.)
* Boolean literal: true and false
* Pointer literal: `nullptr`

### Variables

A variable is a named storage (a range of memory that has a type), which may
also be referred to as object.

Initialization is not assignment.

* Initialization: specify the value at the moment it is created
* Assignment: delete the current value and replace it with a new one

When we define a variable without an initializer, the variable is default
initialized.

* Variables defined outside any function body are initialized to zero
* Variables of built-in type defined inside a function are uninitialized
* Each class controls how we initialize objects of that class type

a declaration is a base type followed by a list of declarators, making a name
known to the program, using `extern`. A definition creates the associated
entity. Variables must be define exactly once but can be declared many times.

A scope is a part of the program in which a name has a particular meaning. Most
scopes in C++ are delimited by curly braces.

* Global scope: `main`
* Block scope

### Compound Types

A compound type is a type that is defined in terms of another type.

A Reference is an alias not an object, and it defines an alternative name for
an object. There is no way to rebind a reference to refer to a different
object, references must be initialized. When we define a reference, instead of
copying the initializer’s value, we bind the reference to its initializer. A
reference may be bound only to an object, not to a literal or to the result of
a more general expression.

A pointer is a compound type, an object, that “points to” another type.

Separate compilation makes it possible to split the programs into several
files, each of which can be compiled independently.

### `const` Qualifier

`const` objects must be initialized.

### Define Our Own Data Structure

* Class data member
* Class function member

In-class initializer (list initialization) is supported by the new standard,
and the data members will be default initialized without in-class initializer.

In order to ensure that the class definition is the same in each file, classes
are usually defined in header files.

The preprocessor is a program that runs before the compiler and changes the
source text of our programs. Header guards are used to make it safe to include a
header multiple times.

* `#define` defines a name as a preprocessor variable
* `#ifdef` is true if the variable has been defined
* `#ifndef` is true if the variable has not been defined
* `#endif`

## Strings, Vectors and Arrays

In general, the library types strive to make it as easy to use a library type
as it is to use a built-in type.

### Library `string` type

A string is a type representing a variable-length sequence of characters.
Strings are usually initialized in the following ways:

```c++
string s1;
string s2(s1);
string s2 = s1;
string s3("hello");
string s3 = "hello"; // The null character is omitted
string s4(10, 'c');
```

Companion type, e.g. `string::size_type`, make it possible to use the library
types in a machine-independent manner.

The `string` library lets convert both character literals and character string
literals to strings.

The `cctype` library offers a rich set of facilities processing a single
character. While subscripting a string, the user has to make sure that the
index does not go outside of the range and the string is not empty.

For most applications, in addition to being safer, it is also more efficient
to use library strings rather than C-style strings.

### Library `vector` type

A vector is a class template, a collection of objects, all of which have the
same type. Templates can be thought of as instructions to the compiler for
instantiate classes or functions. `vector` is a template, not a type. Types
generated from vector must include the element type, for example,
`vector<int>`.

A vector can be initialized in the following ways:

```c++
vector<T> v1; // Default initialization, v1 is empty
vector<T> v2(v1);
vector<T> v2 = v1; // Copy initialization, the constructor is called
vector<T> v3(n,val);
vector<T> v3(n); // Value initialization
vector<T> v5{a,b,c. . . };
vector<T> v5{a,b,c. . . }; // List initialization
```

### Introducing iterator

Like pointers, iterators give indirect access to an object. A valid iterator
either denotes an element or denotes a position one past the last element in a
container.

Iterators are usually initialized by the member functions of types that
supports iterator.

One companion type is defined as `diference_type` for the subtraction of two
iterators.

Binary search using iterators:

```c++
auto beg = text.begin(), end = text.end();
auto mid = text.begin() + (end - beg) / 2;

while (mid != end && *mid != token) {
    if (*beg < token) {
        beg = mid + 1;
    } else {
        end = mid;
    }
    mid = (end - beg) / 2;
}
```

### Arrays

An array is a fixed-size container with compound type offering better
performance and less flexibility compared with a vector. Note that the
dimension is also part of the array type.

By default, `const` objects are local to a file, the compiler substitutes the
variable with its value across the file. In order to share the object across
multiple files, the variable must be defined as `extern const` on both its
definition and declaration(s).

Due to historical reasons, it is not allowed to copy and assign an array with
another array.

Understanding complicated array declaration:

* right to left
* inside out

```c++
int *ptrs[10];
int &refs[10]; // error
int (*Parray)[10];
int (&arrRef)[10];
int *(&arry)[10]; // reference to an array of 10 int pointers
```

`size_t` is a machine-specific unsigned type that is guaranteed to be large
enough to hold the size of any object in memory, defined in `cstddef`. The
result of subtracting two pointers is a library type named `ptrdiff_t`.

In most places when an array is used, the compiler automatically substitutes a
pointer to the first element. Unlike subscripts for vector and string, the
index of the built-in subscript operator is not an unsigned type.

Modern C++ programs should use vectors and iterators instead of built-in arrays
and pointers, and use strings rather than C-style array-based character
strings.

## Expressions

An expression is composed of one or more operands and yields a result when it
is evaluated.

### Fundamentals

Lvalue and Rvalue: roughly speaking, the object’s identity (its location in
memory) is used as a lvalue (locator value), and the object’s value (its
contents) is used as a rvalue. An expression is either a lvalue or a rvalue.
Rvalue is usually a temporary result in same temporary register. An implicit
_lavalue-to-rvalue_ conversion is done when a rvalue is needed, but a rvalue
cannot be converted to lvalue.

Sorted in precedence and left associative.

* Arithmetic Operators
    + `+`: unary plus
    + `-`: unary minus, e.g.: `bool b = true; bool b2 = -b; // b2 is true`
    + `*`: multiplication
    + `/`: division
    + `%`: reminder
    + `+`: addition
    + `-`: subtraction
* Logical and Relational Operators
    + `!`: logical not
    + `<`: less than
    + `<=`: less than or equal
    + `>`: greater than
    + `>=`: greater than or equal
    + `==`: equality
    + `!=`: inequality
    + `&&`: logical and
    + `||`: logical or
* Assignment Operator: the left-hand operand of an assignment operator must be
  a modifiable lvalue. Assignment is right associative.
* Increment and Decrement Operators: usually used with iterators, because many
  of them do not support arithmetic. The prefix operator yields the changed
  object as its result, while the postfix operator yields an unchanged copy.
  Should understand the expression `*iter++`.
* The Member Access Operators: The dot `.` and arrow `->` operators provide for
  member access.
* The `sizeof` Operator: The `sizeof` operator returns the size, in bytes, of
  an expression or a type name.
* The Bitwise Operators:
    + `~`: bitwise `NOT`
    + `<<`: left shift
    + `>>`: right shift
    + `&`: bitwise `AND`
    + `^`: bitwise `XOR`
    + `|`: bitwise `OR`

### Type Conversions

* Arithmetic Conversions: the arithmetic conversions are defined to preserve
  precision, if possible. And then the initializer is converted to the object’s
  type during initialization.
* Array to Pointer Conversions: in most expressions, the array is automatically
  converted to a pointer to the first element in that array. But there are some
  exceptions.
* Pointer Conversions
* Conversions to `bool`
* Conversion to `const`: not possible for low-level `const`
* Conversions Defined by Class Types: e.g. `while (cin >> s)`, converts
  `istream` to `bool`

## Statements

Statements are executed sequentially and more complicated execution paths are
supported with _flow-of-control_ statements.

### Simple Statements

* Null statement: `;`
* Compound statement: statements surrounded by a pair of curly braces

### Conditional Statements

* The `if` statement: `if`, `else`, `else if`, each `else` is matched with the
  closest preceding unmatched `if`, __dangling else__ can be avoided with
  braces
* The `switch` statement: `switch`, `case`, `default`
    + The `case` label must be integral constant expressions
    + It is not allowed to jump over an initialization if the variable is in
      scope at the point to which control transfers

## Generic Algorithms

The library provides a set of generic algorithms, most of which are independent
of any particular container / object type.

### Overview

`algorithm` and `numeric` headers.

In general, the algorithms do not work directly on a container. Instead, they
operate by traversing a range of elements bounded by two iterators.
