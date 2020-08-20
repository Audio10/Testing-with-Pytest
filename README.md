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



## -x, –exitfirst 

Normal pytest behavior is to run every test it finds. If a test function encounters a failing assert or an exception, the execution for that test stops there and the test fails. And then pytest runs the next test. Most of the time, this is what you want. However, especially when debugging a problem, **stopping the entire test session immediately when a test fails** is the right thing to do. That’s what the -x option does.

```bash
pytest -x
```



## –maxfail=num 

The -x option stops after one test failure. If you want to let some failures happen, but not a ton, use the --maxfail option to specify how many failures are okay with you.

```bash
// The test will be stopped when it has 2 fails.
pytest --maxfail=2 --tb=no
```

## -s

The -s flag allows print statements—or really any output that normally would be printed to stdout —to actually be printed to stdout while the tests are running.

**With that you can use prints and view them on the console.** 

```bash
pytest -m run_these_please -s
```



## –lf, –last-failed 

When one or more tests fails, having a convenient way to run just the failing tests is helpful for debugging. Just use --lf and you’re ready to debug:

```bash
pytest --lf
```



## –ff, –failed-first 

The --ff/--failed-first option will do the same as --last-failed, and then run the rest of the tests that passed last time:

```bash
pytest --ff
```

## -l, –showlocals 

If you use the -l/--showlocals option, local variables and their values are displayed with tracebacks for failing tests.

```bash
// Show the value of the variables if we have a error.
pytest -l
```



## –tb=style (Traceback)

The --tb=style option modifies the way tracebacks for failures are output. When a test fails, pytest lists the failures and what’s called a traceback, which shows you the exact line where the failure occurred. Although tracebacks are helpful most of time, there may be times when they get annoying. 

```bash
// It doesn't show the traceback
pytest --tb=no

// It shows the traceback in a line
pytest --tb=line

// It shows a short traceback
pytest --tb=short

// It shows you the most exhaustive, informative traceback possible
pytest --tb=long


```



## –durations=N 

The --durations=N option is incredibly helpful when you’re trying to speed up your test suite. It doesn’t change how your tests are run; it reports the slowest N number of tests/setups/teardowns after the tests run. If you pass in --durations=0, **it reports everything in order of slowest to fastest**.



```
pytest --durations=3
```

