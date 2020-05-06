# Notes on pytest

These notes were taken by [hainesm6](mailto:hainesm6@gmail.com)

- [Notes on pytest](#notes-on-pytest)
  - [Sources](#sources)
  - [General notes](#general-notes)
  - [Syntax](#syntax)
    - [Basic syntax](#basic-syntax)
    - [Marking test functions with decorators](#marking-test-functions-with-decorators)
  - [Coverage](#coverage)
    - [Coverage in pytest](#coverage-in-pytest)
    - [Integration with coveralls.io](#integration-with-coverallsio)

## Sources

1. [Python Testing 101 with pytest](https://www.youtube.com/watch?v=etosV2IWBF0)
2. [The Docs](https://docs.pytest.org/en/latest/contents.html#toc)

## General notes

- What a test/pytest should fulfil:
  - Prove that code works as designed.
  - Provides examples and documentation.
  - As project grows provides an automated system for testing.
- Writing tests before writing code is referred to as **test-driven development (TDD)** and is one strategy for development with associated [advantages and benefits](https://leantesting.com/test-driven-development/).
- When developing and a bug is encountered, rather than diving straight into fixing the bug, first write a test where the desired behaviour is observed. As you make modifications to the API, it is easy to determine when the correct behaviour is observed. Refer to [source 1](#sources).

## Syntax

### Basic syntax

- The **"assert"** statement is the core syntax of pytest.
Modules and functions must be prefixed with "test_".
- To test for a unit of codes ability to throw an error, use the **pytest.raises(*ExpectedException*)** function within a context manager.

```python
>>> with raises(ZeroDivisionError):
        ...    1/0
```

- It is also possible to pass a **match** keyword argument into raises to test the returned exception. This is argument is treated as a regular expression:

```python
>>> with raises(ValueError, match=r'must be \d+$'):
        ...     raise ValueError("value must be 42")
```

### [Marking test functions](https://docs.pytest.org/en/latest/mark.html) with decorators

- The `@pytest.mark` decorator modifies test function behaviour enabling for instance test functions:
  - To be skipped (@pytest.mark.skip).
  - To be skipped if a condition is met (@pytest.mark.skipif).
  - To fail as expected (@pytest.mark.xfail).

An example is:

```python
@pytest.mark.skip(reason="Old test no longer relevant")
def test_old_test():
        ...
```

## Coverage

### Coverage in pytest

- Coverage indicates how much of the code is executed during tests.
- Note, while 100 % code coverage is desirable, it does not indicate whether all code was tested for all possible inputs implying bugs may still exist.
- In pytest, coverage can be measured using the `pytest-coverage` plugin; installed using the pip package manager. It can be implemented as follows:

```shell
python -m pytest -cov [SOURCE1 SOURCE2]
```

where SOURCES are the path or package name for coverage measurement.

### Integration with [coveralls.io](https://github.com/z4r/python-coveralls)

- Suggest to use [Travis CI](https://travis-ci.org/). Add the following to the .travis.yml file:

```yml
after_success:
  - coveralls([SOURCE])
```
