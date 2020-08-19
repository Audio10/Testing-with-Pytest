# Python Testing with Pytest



## Install Pytest

Like other Python packages distributed through PyPI, use pip to install pytest into the virtual environment you’re using for testing: 

```bash
$ pip3 install -U virtualenv 
$ python3 -m virtualenv venv 
$ source venv/bin/activate 

// Install pytest
$ pip install pytest
```



## Pytest's name conventions

The part of pytest execution where pytest goes off and finds which tests to run is called test discovery. pytest was able to find all the tests we wanted it to run because we named them according to the pytest naming conventions. Here’s a brief overview of the naming conventions to keep your test code discoverable by pytest: 

- Test files should be named test_.py or _test.py. _

- Test methods and functions should be named test_

- Test classes should be named Test.



## Run Pytest



```bash
 // Run all the folder
 $ pytest
 
 // Run with details
 $ pytest -v
 
 // Run a file
 $ pytest test_file.py 
 
 // Run just only test in a test_file
 pytest -v tasks/test_four.py::test_asdict
 
 
 
 
```



## Using Options



### --Collect-only

The --collect-only option shows you which tests will be run with the given options and configuration. It’s convenient to show this option first so that the output can be used as a reference for the rest of the examples

The --collect-only option is helpful to check if other options that select tests are correct before running the tests. 

```bash
pytest --collect-only
```



### -k EXPRESSION (Filter by name)

The -k option lets you use an expression to find what test functions to run. Pretty powerful. It can be used as a shortcut to running an individual test if its name is unique, or running a set of tests that have a common prefix or suffix in their names. 

You can use `and`, `or`, `not` and parentheses.

**You can use this to run only the test that matches with the expression.**

```bash
pytest -v -k "asdict or defaults" 
```

Let’s say you want to run the test_asdict() and test_defaults() tests. You can test out the filter with --collect-only:

```bash
 $ cd /path/to/code/ch1
 $ pytest -k "asdict or defaults" --collect-only
 
 // You can use this like a filter
 $ pytest test_four.py -k "asdict or defaults" --collect-only 
```



## -m MARKEXPR

Markers are one of the best ways to mark a subset of your test functions so that they can be run together. As an example, one way to run test_replace() and test_member_access(), even though they are in separate files, is to mark them. 

You can use any marker name. Let’s say you want to use run_these_please. You’d mark a test using the decorator @pytest.mark.run_these_please, like so:

```python
import pytest
...
@pytest.mark.run_these_please
def test_member_access():
...
```

