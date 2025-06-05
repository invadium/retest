# reTest

_A minimalistic bash-powered test anti-framework._


## Intro

What if I tell you, that you can test your system without
a testing framework, using nothing, but a bunch
of shell scripts and plain text files.

With _reTest_ it is possible to setup a minimalistic
testing environment just by dropping a single bash
script into your project's directory.


## Installation


### Download

Just download and place the [_retest_](https://raw.githubusercontent.com/invadium/rebasic/refs/heads/master/retest)
bash script near your test suit folder.

You can use _curl_ for that:
```
    curl https://raw.githubusercontent.com/invadium/retest/master/retest > retest
```

Or _wget_:
```
    wget https://raw.githubusercontent.com/invadium/retest/master/retest
```


### Configure

Add permissions to execute the shell file:
```
    chmod +x retest
```

Now you can run tests grouped in directories. Check out:
```
    ./retest --help
```
for details.



## Test Suit Organization

A test suit is just a folder with test case scripts
doubled by expected result files.

The name of a test case MUST match the name
of the corresponding result file.

```
    testA.py    testA.expect
    testB.py    testB.expect
```

The idea behind _retest_ testing model
is pretty simple - it runs the test case scripts
and matches results with the data placed in *.expect files.
If a result matches expected data, the test passes.
Otherwise, the test fails.

Check out a test suit organization example
for [bash](https://github.com/invadium/retest/tree/master/test)
as well as for other languages.

Look at [some examples](https://github.com/invadium/retest/blob/master/validate)
of how _retest_ can be run for various scenarios.


### Customize test cases source directory

By default, _retest_ will be looking for test cases
in the directory _./test_, but you can specify
the location explicitly:

```bash
    ./retest --path ./test-cases
```

Often, it makes sense to create a substructure
to be able to run test subsets separately:
```
    ./retest -p ./test/set-1
    ./retest -p ./test/set-2
    ./retest -p ./test
```
As you can see, it is possible to split
the test suit on multiple directories and run them
one-by-one or all together.


### Setup test interpreter and test case files extension
_retest_ uses _find_ to locate all test cases
in the test suit. By default, all files with
_'*.case'_ extension.

Test cases are considered to be bash scripts
by default, but you can specify a different
interpreter with _--exec/-x_ option.

Say, we want to execute all *.py files with
_python_ interpreter:

```bash
    ./retest --exec /usr/bin/python --case py
```


### Set expected results file extension
Results of _retest_ execution of a test case
are matched with expected results data.
Expected results file name must match
the name of a test case it is intended for:

```
    ./test/checkA.case == ./test/checkA.expected
    ./test/checkB.case == ./test/checkB.expected
```

You can specify a different extention
for expected results by using _--expect/-e_ option:

```
    ./retest --expect testdata
```


### Configure the Output Details
You have a number of options to configure
the output details.

Use _-v_ or _--verbose_ to list all executed cases
and show failure details.

The _--trace_ option is useful to debug test evaluation results.
The _--source_ option shows the original content
of a test case script that has been evaluated.


### Environment Configuration

Some configuration options can be set over the environment variables.

Note, that command line options take precedence over the variables
from the environment.

Possible environment variables:
```
RETEST_PATH       - a path for test cases lookup
RETEST_EXEC       - an interpreter for test execution
RETEST_CASE_EXT   - a file extention for test cases
RETEST_EXPECT_EXT - a file extention for expected results
```



## Tips

* It is possible to use _retest_ as a global script from _/usr/local/bin_.
* Wrap _retest_ call in a service script to hide the configuration boilerplate.
* Use a wrapper script to export config variables for use in the test cases.



## Real Use Cases

Check out how *reTest* is used in real projects:

* [ReBasic Interpreter](https://github.com/invadium/rebasic) - a reimplementation of an old 80s-styled BASIC for the modern web.

