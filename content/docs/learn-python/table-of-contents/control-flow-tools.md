---
title: Control Flow Tools
weight: 1
---

# Control Flow Tools 

## WHAT is this?

Control flow is **the order in which a program executes statements and instructions, and how it progresses from one instruction to the next**. It's based on logic and conditions.

## WHY is this important?

Control flow allows developers to create flexible and dynamic programs.

## WHY should I learn this?

That allows me respond to inputs, repeat tasks, and make decisions.

## WHEN will I need this?

- **Sequential**: The default mode
- **Selection**: Used to make decisions and branch out, choosing between multiple alternative paths
- **Repetition**: Used for looping, which is repeating a piece of code multiple times in a row

## HOW does this work?

### `if` statements

It selects exactly one of the suites by evaluating the expressions one by one until one is found to be true.

```python
>>> x = int(input("Please input a number:"))
Please input a number:5
>>> if x < 0:
...     x = 0
...     print('Negative change to zero')
... elif x == 0:
...     print('Zero')
... elif x == 1:
...     print('One')
... else:
...     print('More')
...
More
```

An `if` … `elif` … `elif` … sequence is a substitute for the `switch` or `case` statements found in other languages.

### `for` statements

Python’s `for` statement iterates over the items of any sequence (a list or a string), in the order that they appear in the sequence.

```python
>>> words = ['student', 'teacher', 'goat']
>>> for w in words:
...     print(w, len(w))
...
student 7
teacher 7
goat 4
```

Code that modifies a collection while iterating over that same collection can be tricky to get right. Instead, it is usually more straight-forward to loop over a copy of the collection:

```python
>>> users = {'Angli': 'active', 'Adi': 'active', 'Napi': 'inactive'}
>>> for user, status in users.copy().items():
...     if status == 'active':
...             del users[user]
...
>>> users
{'Napi': 'inactive'}
```

### the `range()` function

If you do need to iterate over a sequence of numbers, the built-in function `range()` comes in handy.

```python
>>> range(10)
range(0, 10)
>>> for i in range(5):
...     print(i)
...
0
1
2
3
4
>>> list(range(4, 10))
[4, 5, 6, 7, 8, 9]
>>> list(range(0, 10, 2))
[0, 2, 4, 6, 8]
>>> list(range(-10, -100, -20))
[-10, -30, -50, -70, -90]
>>> a = ['Sony', 'Samsung', 'XL', 'Telkomsel']
>>> for i in range(len(a)):
...     print(i, a[i])
...
0 Sony
1 Samsung
2 XL
3 Telkomsel
>>> sum(range(4))
6
```

In most such cases, however, it is convenient to use the `enumerate()` function.

```python
>>> seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
```

### `break` and `continue` statmenets

```python
>>> for num in range(2, 10):
...     if num % 2 == 0:
...             print(f"found an even number {num}")
...             continue
...     print(f"found an odd number {num}")
...
found an even number 2
found an odd number 3
found an even number 4
found an odd number 5
found an even number 6
found an odd number 7
found an even number 8
found an odd number 9
```

### `else` clauses on loops

In a `for` or `while` loop the break statement may be paired with an `else` clause.

If the loop finishes without executing the `break`, the `else` clause executes.

In a `foor` loop, the else clause is executed after the loop finishes its final iteration, that is, if no break occured

In a `while` loop, it's executed after the loop's condition become false.

Other ways of ending the loop early, such as a `return` or a raised exception.

```python
>>> for n in range(2, 10):
...     for x in range(2, n):
...             if n % x == 0:
...                     print(n, 'equals', x, '*', n//x)
...                     break
...     else:
...             print(n, 'is a prime number')
...
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```

Yes, this is the correct code. Look closely: the `else` clause belongs to the `for` loop, **not** the if statement.

### `pass` statements

The `pass` statement does nothing. It can be used when a statement is required syntactically but the program requires no action. For example:

```python
>>> while True:
...     pass # Busy-wait for keyboard interrupt (C-c)
```

This is commonly used for creating minimal classes:

```python
>>> class EmptyClass:
...     pass
```
Another place `pass` can be used is as a place-holder for a function or conditional body when you are working on new code, allowing you to keep thinking at a more abstract level. The pass is silently ignored:

```python
>>> def initlog(*args):
...     pass # NOTE: remember to implement this!
...
```

### `match` statements

A `match` statement takes an expression and compares its value to successive patterns given as one or more case blocks.

Only the first pattern that matches gets executed and it can also extract components (sequence elements or object attributes) from the value into variables.

The “variable name” `_` acts as a wildcard and never fails to match. If no case matches, none of the branches is executed.

```python
>>> def http_error(status):
...     match status:
...             case 400:
...                     return "Bad request"
...             case 404:
...                     return "Not found"
...             case 418:
...                     return "I'm a teapot"
...             case _:
...                     return "Something's wrong with the internet"
...
>>> http_error(404)
'Not found'
>>> http_error(500)
"Something's wrong with the internet"
```

You can combine several literals in a single pattern using | (“or”)

```python
case 401 | 403 | 404:
    return "Not allowed"
```

Patterns can look like unpacking assignments, and can be used to bind variables

```python
>>> point = (2, 3)
>>> match point:
...     case (0, 0):
...             print("Origin")
...     case (0, y):
...             print(f"Y={y}")
...     case (x, 0):
...             print(f"X={x}")
...     case (x, y):
...             print(f"X={x}, Y={y}")
...     case _:
...             raise ValueError("Not a point")
...
X=2, Y=3
```

### defining functions

The keyword `def` introduces a function definition.

It must be followed by the function name and the parenthesized list of formal parameters.

The statements that form the body of the function start at the next line, and must be indented.

The first statement of the function body can optionally be a string literal; this string literal is the function’s documentation string, or docstring. 

The `return` statement returns with a value from a function. return without an expression argument returns `None`. Falling off the end of a function also returns `None`.

```python
>>> def fib(n):
...     """Print a Fibonacci series less than n."""
...     a, b = 0, 1
...     while a < n:
...             print(a, end=' ')
...             a, b = b, a + b
...     print()
...
>>> # call the function
>>> fib(2000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597
>>> fib
<function fib at 0x103140b80>
>>> f = fib
>>> f(1000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
>>> fib(0)

>>> print(fib(0))

None
>>> def fib2(n):
...     """Return a list containing the Fibonacci series up to n."""
...     result = []
...     a, b = 0, 1
...     while a < n:
...             result.append(a)
...             a, b = b, a + b
...     return result
...
>>> f100 = fib2(100)
>>> f100
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
>>> fib2(200)
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144]
```

### more on defining functions

It is also possible to define functions with a variable number of arguments. There are three forms, which can be combined.

#### default argument values

```python
>>> def ask_ok(prompt, retries=4, reminder='Please try again!'):
...     while True:
...         reply = input(prompt)
...         if reply in {'y', 'ye', 'yes'}:
...             return True
...         if reply in {'n', 'no', 'nop', 'nope'}:
...             return False
...         retries = retries - 1
...         if retries < 0:
...             raise ValueError('invalid user response')
...         print(reminder)
...
>>> ask_ok('Do you really want to quit?')
Do you really want to quit?y
True
>>> ask_ok('OK to overwrite the file?', 2)
OK to overwrite the file?n
False
>>> ask_ok('OK to overwrite the file?', 2)
OK to overwrite the file?a
Please try again!
OK to overwrite the file?a
Please try again!
OK to overwrite the file?a
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 10, in ask_ok
ValueError: invalid user response
>>> ask_ok('OK to overwrite the file?', 2, 'Come on, only yes or no!')
OK to overwrite the file?a
Come on, only yes or no!
OK to overwrite the file?a
Come on, only yes or no!
OK to overwrite the file?a
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 10, in ask_ok
ValueError: invalid user response
```

#### keyword arguments

Functions can also be called using keyword arguments of the form `kwarg=value`.

When a final formal parameter of the form `**name` is present, it receives a dictionary containing all keyword arguments except for those corresponding to a formal parameter.

This may be combined with a formal parameter of the form `*name` which receives a tuple containing the positional arguments beyond the formal parameter list.

```python
>>> def cheeseshop(kind, *arguments, **keywords):
...     print("-- Do you have any", kind, "?")
...     print("-- I'm sorry, we're all out of", kind)
...     for arg in arguments:
...         print(arg)
...     print("-" * 40)
...     for kw in keywords:
...         print(kw, ":", keywords[kw])
...
>>> cheeseshop("Limburger", "It's very runny, sir.",
...            "It's really very, VERY runny, sir.",
...            shopkeeper="Michael Palin",
...            client="John Cleese",
...            sketch="Cheese Shop Sketch")
-- Do you have any Limburger ?
-- I'm sorry, we're all out of Limburger
It's very runny, sir.
It's really very, VERY runny, sir.
----------------------------------------
shopkeeper : Michael Palin
client : John Cleese
sketch : Cheese Shop Sketch
```

#### special parameters

By default, arguments may be passed to a Python function either by position or explicitly by keyword. For readability and performance, it makes sense to restrict the way arguments can be passed so that a developer need only look at the function definition to determine if items are passed by position, by position or keyword, or by keyword.

```
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
```

```python
>>> def standard_arg(arg):
...     print(arg)
...
>>> def pos_only_arg(arg, /):
...     print(arg)
...
>>> def kwd_only_arg(*, arg):
...     print(arg)
...
>>> def combined_example(pos_only, /, standard, *, kwd_only):
...     print(pos_only, standard, kwd_only)
...
```

**standard**

```python
>>> standard_arg(2)
2
>>> standard_arg(arg=2)
2
```

**positional-only**

```python
>>> pos_only_arg(1)
1
>>> pos_only_arg(arg=1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: pos_only_arg() got some positional-only arguments passed as keyword arguments: 'arg'
```

**keyword-only**

```python
>>> kwd_only_arg(3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: kwd_only_arg() takes 0 positional arguments but 1 was given
>>> kwd_only_arg(arg=3)
3
```

**positional-or-keyword**

```python
>>> combined_example(1, 2, 3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: combined_example() takes 2 positional arguments but 3 were given
>>> combined_example(1, 2, kwd_only=3)
1 2 3
>>> combined_example(1, standard=2, kwd_only=3)
1 2 3
>>> combined_example(pos_only=1, standard=2, kwd_only=3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: combined_example() got some positional-only arguments passed as keyword arguments: 'pos_only'
```

**As guidance**:

- Use positional-only if you want the name of the parameters to not be available to the user. This is useful when parameter names have no real meaning, if you want to enforce the order of the arguments when the function is called or if you need to take some positional parameters and arbitrary keywords.

- Use keyword-only when names have meaning and the function definition is more understandable by being explicit with names or you want to prevent users relying on the position of the argument being passed.

- For an API, use positional-only to prevent breaking API changes if the parameter’s name is modified in the future.

### arbitary argument lists

Normally, these *variadic* arguments will be last in the list of formal parameters, because they scoop up all remaining input arguments that are passed to the function. Any formal parameters which occur after the `*args` parameter are ‘keyword-only’ arguments, meaning that they can only be used as keywords rather than positional arguments.

```python
>>> def concat(*args, sep="/"):
...     return sep.join(args)
...
>>> concat("godean", "jetis", "kasongan")
'godean/jetis/kasongan'
>>> concat("godean", "jetis", "kasongan", sep=".")
'godean.jetis.kasongan'
```

### unpacking argument lists

The reverse situation occurs when the arguments are already in a list or tuple but need to be unpacked for a function call requiring separate positional arguments.

the function call with the `*`-operator to unpack the arguments out of a list or tuple

```python
>>> list(range(3, 6))
[3, 4, 5]
>>> args = [3, 6]
>>> list(range(*args))
[3, 4, 5]
```

In the same fashion, dictionaries can deliver keyword arguments with the `**`-operator

```python
>>> def parrot(voltage, state='a stiff', action='voom'):
...     print("-- This parrot wouldn't", action, end=' ')
...     print("if you put", voltage, "volts through it.", end=' ')
...     print("E's", state, "!")
...
>>> d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
>>> parrot(**d)
-- This parrot wouldn't VOOM if you put four million volts through it. E's bleedin' demised !

```

### lambda expressions

Small anonymous functions can be created with the lambda keyword. Lambda functions can be used wherever function objects are required. They are syntactically restricted to a single expression. Semantically, they are just syntactic sugar for a normal function definition. Like nested function definitions, lambda functions can reference variables from the containing scope:

```python
>>> def make_incrementor(n):
...     return lambda x: x + n
...
>>> f = make_incrementor(42)
>>> f(0)
42
>>> f(1)
43
```

The above example uses a lambda expression to return a function. Another use is to pass a small function as an argument:

```python
>>> pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
>>> pairs.sort(key=lambda pair: pair[1])
>>> pairs
[(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
```

### documentation strings

```python
>>> def my_function():
...     """Do nothing, but document it.
...
...     No, really, it doesn't do anything.
...     """
...     pass
...
>>> print(my_function.__doc__)
Do nothing, but document it.

    No, really, it doesn't do anything.

```

### function annotations

Function annotations are completely optional metadata information about the types used by user-defined functions.

Annotations are stored in the `__annotations__` attribute of the function as a dictionary and have no effect on any other part of the function. 

Parameter annotations are defined by a colon after the parameter name, followed by an expression evaluating to the value of the annotation. 

Return annotations are defined by a literal `->`, followed by an expression, between the parameter list and the colon denoting the end of the def statement.


```python
>>> def f(ham: str, eggs: str = 'eggs') -> str:
...     print("Annotations:", f.__annotations__)
...     print("Arguments:", ham, eggs)
...     return ham + ' and ' + eggs
...
>>> f('spam')
Annotations: {'ham': <class 'str'>, 'eggs': <class 'str'>, 'return': <class 'str'>}
Arguments: spam eggs
'spam and eggs'
```

## Intermezzo: Coding Style

Most languages can be written (or more concise, formatted) in different styles; some are more readable than others. 

Making it easy for others to read your code is always a good idea, and adopting a nice coding style helps tremendously for that.

For Python, [PEP 8](https://peps.python.org/pep-0008/) has emerged as the style guide that most projects adhere to; it promotes a very readable and eye-pleasing coding style.

Every Python developer should read it at some point; here are the most important points extracted for you:

- Use 4-space indentation, and no tabs.

    4 spaces are a good compromise between small indentation (allows greater nesting depth) and large indentation (easier to read). Tabs introduce confusion, and are best left out.

- Wrap lines so that they don't exceed 79 characters.

    This helps users with small displays and makes it possible to have several code files side-by-side on larger displays.

- Use blank lines to separate functions and classes, and larger blocks of code inside functions.

- When possible, put comments on a line of their own.

- Use docstrings.

- Use spaces around operator and after commas, but not directly inside bracketing constructs: `a = f(1, 2) + g(3, 4)`.

- Name your classes and functions consistently; the convention is to use `UpperCamelCase` for classes and `lowercase_snake_case` for functions and methods. Always use `self` as the name for first method argument.

- Don't use fancy encodings if your code is meant to be used in international environtments. Python's default, UTF-8, or even plain ASCII work best in any case.

- Likewise, don't use non-ASCII characters in identifiers if there is only the slightest chance people speaking a different language will read or maintain the code.














