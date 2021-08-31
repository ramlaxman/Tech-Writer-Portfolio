# Modules vs Packages vs Libraries in Python

Generally, object oriented programming languages have some common terms such as `module`, `package`, `library` etc. Though developers use these terms interchangeably as per convenience, each term has its meaning. We'll see details and relation with Python in this article.

## Module

As per dictionary meaning, `module` is a self-contained component (unit or item) which is used in combination with other components. In Python, a module is a `.py` file that defines one or more function or classes which intend to reuse in different codes of an program or softwares.

To reuse the functions of a given module, we simply need to import the module using:

```py
- import <modulename> # to import the entire module
- from <modulename> import <classname> # imports a class from a module
```

Python interpreter treats the filename as the module name. Internally, the name of the module is stored in the namespace as a string type. The module name can be called within the module by calling the global variable `__name__`.

## Package

Suppose, you placed an order for a potato chips. When you received chips, it was wrapped in the package. You opened it and found your chips packet inside the package. In short, you received the `package` of chips. From this example, we can tell `package` is an entity that holds other data or items inside of it. In the similar way, Python package refers to a directory of Python module(s). This feature comes handy for organizing modules of one type at one place. A python package is normally installed at following locations:

- Linux: `/usr/lib/python/site-packages`
- Windows: `C:/Python3/Lib/site-packages/`

We can see this image of `jinja2` package with several `.py` files:

![Example of Jinja2 package](https://raw.githubusercontent.com/ramlaxman/Tech-Writer-Portfolio/main/images/Package%20in%20Python.png)

To use the package in a script, we will have to first initialize the package using:

`mypackage/__init__.pymypackage/mymodule.py` 

we can then import the package:

`import mypackage.mymodule`
or
`from mypackage.mymodule import myclass`

In addition to this, Python is now a powerhouse of large and increasing collection of packages, available at the [Python Package Index](https://pypi.org/).

## Library

In general, we know that library is the place which helps to maintain collections of different books. Similarly, in Python, it is collection of specific syntax, token and semantics intended to perform dedicated tasks.

Library term does not have fixed meaning in Python. It can be the collection of some core modules or group of Python source files for performing dedicated functions. Hence, library is blurred term to define compare to modules and packages. 

`Python standard library`: It is set of libraries that comes with core Python setup. It aims at providing specific functionality to programmers. Also, it does not require separate download and install. For example, `string` , `os`. Libraries contain core modules are written in C languages which are targeted towards system level  functionality.

`Third party library`: Python also supports additional libraries, written in Python, that provide extra features and functionalities apart from Python standard library. In more general manner, we can call them as `pacakges`.
Note that these libraries require separate download and installation. Check [Python package index](https://pypi.python.org) for more details.

**Some tips:**

1. Do not install libraries using Python source code unless you're testing against current version of Python or operating system environment.  

2. Before installing with `pip`, check with the package site which Python version it supports.

3. Installation using `pip`

   Consider, we want to install `pymongo`, a python client for MongoDB. Following are some operations, we can perform using `pip`:

   To install latest version
   ```powershell
   $ python -m pip install pymongo
   ```

   To get a specific version of pymongo
   ```powershell
   $ python -m pip install pymongo==3.1.1
   ```

   To upgrade pymongo
   ```powershell
   $ python -m pip install --upgrade pymongo
   ```

   To uninstall
   ```powershell
   $ python -m pip uninstall pymongo
    ```

4. Use `.whl` files for installation if there is no Internet access:

```py
C:/> pip install Flask-2.0.1-py3-none-any.whl
```

Thanks for reading.