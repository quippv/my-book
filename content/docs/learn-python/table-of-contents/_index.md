---
weight: 10
bookCollapseSection: true
---

# Python Interpreter

## WHAT is this?

The Python interpreter is usually installed as `/usr/local/bin/python3.13` on those machines where it is available.

Since the choice of the directory where the interpreter lives is an installation option, other places are possible; check with your local Python guru or system administrator.

---

### My version:

We can use `which python` to find the python interpreter folder location.

## WHY is this important?

### My version:

To translate your Python code for a computer machine (run code).

## WHY should i learn this?

The interpreter is said to be in interactive mode.

## WHEN will I need this?

### My version:

Run Python code interactively.

## HOW does this work?

Start it by typing the command on terminal:

```bash
python
```

By default, Python source files are treated as encoded in UTF-8. In that encoding, characters of most languages in the world can be used simultaneously in string literals, identifiers and comments — although the standard library only uses ASCII characters for identifiers, a convention that any portable code should follow. To display all these characters properly, your editor must recognize that the file is UTF-8, and it must use a font that supports all the characters in the file.

When known to the interpreter, the script name and additional arguments thereafter are turned into a list of strings and assigned to the `argv` variable in the `sys` module. You can access this list by executing `import sys`. The length of the list is at least one; when no script and no arguments are given, `sys.argv[0]` is an empty string. When the script name is given as `'-'` (meaning standard input), `sys.argv[0]` is set to `'-'`.
