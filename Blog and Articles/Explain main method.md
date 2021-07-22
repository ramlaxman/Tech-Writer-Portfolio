# Main method and operators in C++

## About this article:

These are short notes on basic concepts of C++. We'll cover following topics:

- What is the meaning of `using namespace std` ?

- Prefix and postfix operators

- Basic terminologies in C++

### What is the meaning of *using namespace std*?

In C++, we see following line in every program.

```c++
using namespace std; 
```

Most of the developers consider this as standard declaration that often followed by `main()` method, which is not completely true.
As clearly state in A Tour of C++,a book by Bjarne Stroustroup,
`std` should not use independently. It should 

`namespace`  - isolate and virtualize system resources

To organize variables, if they are numerous, namespaces are used.

`using` and `namespace` are keywords.

`Std` is a specific part of the standard library in C++.

`Std` is a predefined namespace of C++ includes methods such as count, cin, string, vector, map.

### Prefix and Postfix

> ++p is called pre increment operation while p++ is called post increment operation.

The main difference lies in the way they behave during assignment.Let us understand their difference with an example:

Suppose `p = 5`;

When we assign `x=++p`,

the increment operation is carried out first and then the value of p is assigned to x. So both p and x are set to 6.

```c++
// Prefix
p = 6
x = 6
```

When we assign `x=p++`, 

the increment operation is carried out ***after*** the value of p is assigned to x. So, x is set to 5 while p is incremented to 6.

```c++
// Postfix
x = 5
p = 6
```

class: group of things having something common connection
object: things to which actions directions
instance:  example of class
members: part of structure
field: area of activity
method: orderliness step by step things
statement: expressing state in words
state: condition something in 
parameter: limit defining scope of activity
overload: Put too great demand on 
constant: value not compute or recompute for whole lifetime of program.
named constant:  name that you have given to constant 
