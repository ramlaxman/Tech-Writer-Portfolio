# Short Notes on C++

## About this article

These are short notes on basic concepts of C++. We'll see following topics:

- What is the meaning of `using namespace std` ?

- Prefix and postfix operators

- Meaning of keywords in C++

### **What is the meaning of *using namespace std* ?**

In C++, we see following line in every program.

```c++
using namespace std; 
```

Most of the developers consider this as standard declaration that often followed by `main()` method, which is not completely true. 

When programmer uses `std` independently, it creates confusion among other programmers and readers. It should always use in terms of either `namespace` or scope resolution operator denoted by `::`.

Let's understand the meaning of keywords first. 

In the above statement, `using` and `namespace` are keywords while `std` is standard library in C++.

As per book *A Tour of C++*<sup><a href="#1">[1]</a></sup>, `using namespace std;` indicates to make names available from `std` library without using scope resolution.

To organize numerous variables, `namespace` is used. `std` is a specific part of the standard library in C++. In other terms, `std` also includes predefined namespace of C++ having methods such as `cout`, `cin`, `string`, `vector`, `map`.

### **Prefix and Postfix Operators**

> ++p is called pre increment operation while p++ is called post increment operation.

The main difference is the order of assignment. Let us understand their difference with an example:

Suppose `p=5` ,

When we assign `x=++p`,

the increment operation carries out ***first*** and then the value of p gets assigned to x. So both p and x are set to 6.

```c++
// Prefix
p = 6
x = 6
```

When we assign `x=p++`, 

the increment operation carries out ***after*** the value of p is assigned to x. So, x is set to 5 while p is incremented to 6.

```c++
// Postfix
x = 5
p = 6
```

### **Meaning of keywords in C++**

`class`: group of things having something common connections \
`object`: things to which actions are directed \
`instance`: example of class \
`method`: orderliness of step by step activity \
`members`: part of structure or method \
`field`: area of activity \
`statement`: expressing state in words \
`parameter`: limit defining scope of activity \
`constant`: not to compute or recompute value for whole lifetime of program \
`named constant`: name that you have given to constant

<h4 id="1">References</h4>
[1] Stroustrup, Bjarne. A Tour of C++. Addison-Wesley Professional, 2018.