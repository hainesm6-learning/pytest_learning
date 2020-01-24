# Notes on pytest

These notes were taken by [hainesm6](mailto:hainesm6@gmail.com).

## Sources

1. [Python Testing 101 with pytest](https://www.youtube.com/watch?v=etosV2IWBF0)
2. [The Docs](https://docs.pytest.org/en/latest/contents.html#toc)

## General notes

- What a test/pytest should fulfil:
  - Prove that code works as designed.
  - Provides examples and documentation.
  - As project grows provides an automated system for testing.
- Writing tests before writing code is referred to as **test-driven development (TDD)** and is one strategy for development with associated [advantages and benefits](https://leantesting.com/test-driven-development/).
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

- When developing and a bug is encountered, rather than diving straight into fixing the bug, first write a test where the desired behaviour is observed. As you make modifications to the API, it is easy to determine when the correct behaviour is observed. Refer to [source 1](#sources).
