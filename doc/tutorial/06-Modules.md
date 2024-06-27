# Modules and Packages

References:

- [1] Martelli, et al. *Python in a Nutshell, 4th Edition*. 2023. O'Reilly Media, Inc.

A typical Python program is made up of several source files. Each source file is a *module* [&hellip;]. Sometimes, to manage complexity, developers group together related modules into a *package* &mdash; a hierarchical, tree-like structure of related modules and sub-packages. (&sect; 7, [1])

## Modules

A module is a file containing Python definitions and statements. The file name is the module name with the suffix `.py` appended.

```python
# fibonacci.py
def series(n):  # return Fibonacci series up to n
  result = []
  a, b = 0, 1
  while a < n:
    result.append(a)
    a, b = b, a+b
  return result
```

With the Python interpreter,

```python
>>> import fibonacci
```

This does not add the names of the functions defined in ``fibonacci`` directly to the current namespace; it only adds the module name `fibonacci` there. Using the module name you can access the functions:

```python
>>> fibonacci.series(100)
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
```

Modules in Python are handled like other objects. (Module Objects, &sect; 7, [1])

- Thus, you can pass a module as an argument in a call to a function.
- Similarly, a function can return a module as the result of a call.
- A module, just like any other object, can be bound to a variable, an item in a container, or an attribute of an object.
- Modules can be keys or values in a dictionary, and can be members of a set. For example, the `sys.modules` dictionary holds module objects as its values.

```python
>>> import fibonacci as fib
>>> fib.series(100)
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
```

Python also supports *extension modules* &mdash; modules coded in other languages such as C, C++, Java, C#, or Rust. For the Python code importing a module, it does not matter whether the module is pure Python or an extension. (&sect; 7, [1])

The `import` statement is often a better choice than the `from` statement. When you always access module `M` with the statement `import M`, and always access `M`’s attributes with the explicit syntax `M.A`, your code is slightly less concise but far clearer and more readable. One good use of `from` is to import specific modules from a package. In most other cases, `import` is better style than `from`. (`from` versus `import`, &sect; 7, [1])

### Built-ins

The term *built-in* has more than one meaning in Python. (&sect; 8, [1])

- In many contexts, built-in means an object directly accessible to Python code without an `import` statement.
- Some modules are called built-in because they’re in the Python standard library (though it takes an `import` statement to use them).

Data values in Python are known as *objects*; each object, aka *value*, has a *type*. An object’s type determines (Data Types, &sect; 3, [1])

- which operations the object supports (in other words, which operations you can perform on the value).
- the object’s attributes and items (if any) and
- whether the object can be altered

Python has built-in types for [fundamental data types](https://docs.python.org/3/library/stdtypes.html) such as numbers, strings, tuples, lists, dictionaries, and sets:

- numeric types: `int`, `float`, `complex`
- boolean type: `bool`
- sequence types: `list`, `tuple`, `range`
- text sequence type: `str`
- binary sequence types: `bytes`, `bytearray`, `memoryview`
- set types: `set`, `frozenset`
- mapping type: `dict`

### The Module Search Path

When a module named `spam` is imported, the interpreter first searches for a built-in module with that name. These module names are listed in `sys.builtin_module_names`. If not found, it then searches for a file named `spam.py` in a list of directories given by the variable `sys.path`.

- `sys.builtin_module_names`: A tuple of strings containing the names of all modules that are compiled into this Python interpreter.
- `sys.stdlib_module_names`: A frozenset of strings containing the names of standard library modules.

[`sys.path`](https://docs.python.org/3/library/sys.html#sys.path) is a list of strings that specifies the search path for modules. Initialized from the environment variable `PYTHONPATH`, plus an installation-dependent default. By default, as initialized upon program startup, a potentially unsafe path is prepended to `sys.path`:

- `python -m module` command line: prepend the current working directory.
- `python script.py` command line: prepend the script’s directory.
- `python -c code` and `python` (REPL) command lines: prepend an empty string, which means the current working directory.


