# Modules vs Packages vs Libraries in Python

Differences essential to understand

The terms ‘module’, ‘package’ & ‘library’ have different meaning as per type of programming language. Though developers use these terms interchangeably as per convenience, each term has its significance in its own context.

Here’s how these three terms are used in context of python:

## Module

If we see a dictionary meaning, Module is a self-contained component (unit or item) that is used in combination with other components. Simply put, a module in python is a .py file that defines one or more function/classes which you intend to reuse in different codes of your program.

To reuse the functions of a given module you simply need to import the module using:

```py
import <modulename> # to import the entire module

from <modulename> import <classname> # imports a class from a module
```

Python interpreter treats the filename as the module name. 

Internally, the name of the  module is stored in the namespace as a string type. The module name can be called within the module by calling the global variable `__name__`.

## Package

Something we call from outside.  Take an example of courier parcel we order from Internet. It's a third party entity. 
A Python package refers to a directory of Python module(s). This feature comes in handy for organizing modules of one type at one place. A python package is normally installed in:

/usr/lib/python/site-packages # for Linux

C:/Python3/Lib/site-packages/ # for Windows

To use the package in a script, you will have to first initialize the package using:

`mypackage/__init__.pymypackage/mymodule.py` 

You can then import the package

`import mypackage.mymodule`
or
`from mypackage.mymodule import myclass`

In addition to creating ones own packages, Python is home a large and growing collection of packages (from individual programmers) which is available from the Python Package Index.

## Library

Library is the place which helps us to maintain collections of different books. In the similar way, in python, there is a collection of specific syntax, token and semantics in order to perform specific tasks in Python.

Unlike C or C++, the term library does not have any specific contextual meaning in p\Python. When used in Python, a library is used loosely to describe a collection of the core modules.

The term ‘standard library‘ in Python language refers to the collection of exact syntax, token and semantics of the Python language which comes bundled with the core Python distribution.

In Python, the standard library is written in C language and it handles the standard functionalities like file I/O and other core modules that make Python what it is. The python standard library lists down more than 200 such core modules that form the core of Python.

“Additional libraries” refer to those optional components that are commonly included in Python distributions.

The Python installers for the Windows automatically adds the standard library and some additional libraries.

For Unix-like operating systems, the additional library is generally provided as a collection of packages. In Unix Os, one may have to use packaging tools like easyinstall or pip to use these additional libraries.

Don't go by the route of Python Source code unless you are digging into code. i.e. compilation and installation.
Use .whl files for installation with command. C:/> pip install flask****.whl
Before installing with pip, check with the site which Python version it supports.
Install egg files with : easy_install -Z pygame-*.egg

Installing with pip

We recommend using pip to install pymongo on all platforms:
$ python -m pip install pymongo

To get a specific version of pymongo:
$ python -m pip install pymongo==3.1.1

To upgrade using pip:
$ python -m pip install --upgrade pymongo

To uninstall
$ python -m pip uninstall pymongo
