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
`maths.py`:

```python
def square(x):
    return x ** 2
```

Then, elsewhere in your package, you should have a file `test_maths.py` with
the following function definition:

```python
from maths import square
def test_square():
    x = 4
    assert square(x) == 16
```

A whole slew of testing frameworks, such as
[nose](https://nose.readthedocs.org/en/latest/), will then traverse your
project, look for files and functions whose names begin with `test_`, run them,
and report any errors or assertion failures.

I've chosen to use py.test as my framework because:

- it is a strict superset of both nose and Python's built-in unittest, so that
  if you run it on projects set up with those, it'll work out of the box;
- its output is more readable than nose's; and
- its [fixtures]() provide a very nice syntax for test setup and cleanup.

For a quick intro to py.test, you can watch XY's talk at this year's
EuroPython conference:



But the basics are very simple: sprinkle files named `test_something.py`
throughout your project, each containing one or more `test_function()`
definition; then type `py.test` on the command line (at your project root
directory), and voila! Pytest will traverse all your subdirectories, gather up
all the test files and functions, and run your tests.

Here's the output for the minimal `maths` project described above:

```
 ~/projects/maths $ py.test
============================= test session starts ==============================
platform darwin -- Python 2.7.8 -- py-1.4.20 -- pytest-2.5.2
collected 1 items

test_maths.py .

=========================== 1 passed in 0.03 seconds ===========================
```

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

```
 ~/projects/maths $ py.test --doctest-modules
============================= test session starts ==============================
platform darwin -- Python 2.7.8 -- py-1.4.20 -- pytest-2.5.2
collected 2 items

maths.py .
test_maths.py .

=========================== 2 passed in 0.06 seconds ===========================
```

## Test coverage

For small projects, it's easy to check what you have automatically tested. For
bigger projects, you need tools that automatically check what parts of your
code are actually testing. The proportion of lines of code that are run at
least once during your tests is called your *test coverage*.

For the same reasons that testing is important, measuring coverage is
important. Pytest can measure coverage for you with the coverage plugin, found
in the [pytest-cov](https://pypi.python.org/pypi/pytest-cov) package. Once
you've installed the extension, a test coverage measurement is just a
command-line option away:

```
$ py.test --doctest-modules --cov .
```

(The `--cov` takes a directory as input, which I find obnoxious, given that
py.test so naturally defaults to the current directory. But it is what it is.)

With one more option, `--cov-report`, you can see which lines you *haven't*
covered, so you can try to design tests to cover those cases.

Do note that 100% coverage does not ensure correctness. For example, suppose
during a refactor my `square` function ends up looking like so:

```python
def square(x):
    return x * 2
```

I've made a typo, forgetting a ` * ` character. That's cool, I'm
covering that function with a test:

```python
def test_square():
    assert square(2) == 4
```

Oops! Although I have full test coverage, I've missed an error.
But with that caveat in mind, full test coverage is a wonderful thing, and if
you don't test something, you're *guaranteed* not to spot errors in it.

## Turn on continuous integration with Travis

Having tests is great, but it does you no good if you don't remember to run
them. [Travis-CI](https://travis-ci.org) can help!

"Continuous integration" is
the practice of frequently running your test suite so that you never introduce
long-lived bugs into your codebase. Once upon a time, the common practice was
to pile on new features on a codebase. Then, come release time, there would be
a feature freeze, and some time would be spent cleaning up code and removing
bugs. In continuous integration, instead, no new feature is allowed into the
codebase until it is (mostly) bug free, as demonstrated by the test suite.

Travis CI is an online service that integrates with GitHub to run your test
suite *each and every time* you commit code! This way you detect failures early
and can correct them before you pile on too much dependent code, which could
make debugging much more difficult.

Turning on Travis for your own GitHub-hosted projects is pretty easy.
