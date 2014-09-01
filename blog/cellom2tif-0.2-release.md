# The basics of automatic testing for Python projects, with py.test, Travis, and Coveralls

... Plus, announcing the 0.2 release of cellom2tif, a Python package to convert
Cellomics datasets to TIFF.

I've finally decided to do a (small) Python project right, *from scratch*. This
means writing unit tests, setting up continuous integration with Travis (which
runs the tests automatically after each push to your GitHub repo), and setting
up automated test coverage measurements with Coveralls. All of these tools are
completely free for open source projects.

Read on for a brief overview of how to set these things up for your own
projects.

## Automated tests, and why you need them

Software engineering is hard, and it's incredibly easy to mess things up, so
you should write *tests* for all your functions, which ensure that nothing
obviously stupid is going wrong. Tests can take a lot of different forms, but
here's a really basic example. Suppose this is a function in your file,
`math.py`:

```python
def square(x):
    return x ** 2
```

Then, elsewhere in your package, you can have a file `test_math.py` with the
following function definition:

```python
def test_square():
    x = 4
    assert square(x) == 16
```

A whole slew of testing frameworks, such as
[nose](https://nose.readthedocs.org/en/latest/), will then traverse your
project, look for functions whose names begin with `test_`, run them, and
report any errors or assertion failures.

I've chosen to use py.test as my framework because:

- it is a strict superset of both nose and Python's built-in unittest, so that
  if you run it on projects set up with those, it'll work out of the box,
- its output is more readable than nose's, and
- its [fixtures]() provide a very nice syntax for test setup and cleanup.

For a quick intro to py.test, you can watch XY's talk at this year's
EuroPython conference:



But the basics are very simple: sprinkle files named `test_something.py`
throughout your project, each containing one or more `test_function()`
definition; then type `py.test` on the command line (at your project root
directory), and Pytest will traverse all your subdirectories, gather up all the
test files and functions, and run your tests.

In addition to the test functions described above, there is a Python standard
called [doctest]() in which properly formatted usage examples in your
documentation are automatically run as tests. Here's an example:

```python
def square(x):
    """Return the square of a number `x`.

    [...]

    Examples
    --------
    >>> square(5)
    25
    """
    return x ** 2
```

(See my post on [NumPy docstring conventions]() for what should go in the
ellipsis above.)

Depending the complexity of your code, doctests, test functions, or both will
be the appropriate route. py.test supports doctests with the
`--doctest-modules` flag. (This runs both your standard tests *and* doctests.)

## Test coverage

For small projects, it's easy to check what you have automatically tested. For
bigger projects, you need tools that automatically check your *test coverage.*
This is the percentage of lines of code that are executed at least once during
your automated tests.

For the same reasons that testing is important, measuring coverage is
important. However, 100% coverage does not ensure correctness. For example:

```python
def square(x):
    return x * 2
```

Above, I've made a typo, forgetting a ` * ` character. That's cool, I'm
covering that function with a test:

```python
def test_square():
    assert square(2) == 4
```

As you can see, although I have full test coverage, I've missed an error.

Having that caveat in mind, full test coverage is a wonderful thing. py.test
can measure coverage for you with the coverage plugin, found in the
[pytest-cov](https://pypi.python.org/pypi/pytest-cov) package. Once you've
installed the extension, a test coverage measurement is just a command-line
option away:

```
$ py.test --doctest-modules --cov .
```

(The `--cov` takes a directory as input, which I find obnoxious, given that
py.test so naturally defaults to the current directory, but there you go.)

With one more option, `--cov-report`, 
