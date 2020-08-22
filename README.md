# ReTest

_A minimalistic bash-powered test anti-framework._

## Intro

What if I tell you, that you can test your system without
a testing framework using nothing, but a single shell script
and a bunch of plain text files.

With ReTest it is possible to setup a minimalistic
testing environment just by dropping a single shell
script into your project's directory.

## Test Suit Organization

A test suit is just a folder with test case scripts
and expected result files.

### Customize test cases source directory

By default, _retest_ will be looking for test cases
in the directory _./test_, but you can specify
the location explicitly:

```bash
    ./retest --path ./test-cases
    ./retest -p ./test/set-1
    ./retest -p ./test/set-2
```

### Setup test interpreter and test case files extension
_retest_ uses _find_ to locate all test cases
in the test suit. By default, all files with
_'*.case'_ extension.

Test cases are considered to be bash scripts
by default, but you can specify different
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

Note, that command line options are take precedence over the onces
from the environment.

Possible environment variables:
```
RETEST_PATH       - a path for test cases lookup
RETEST_EXEC       - an interpreter for test execution
RETEST_CASE_EXT   - a file extention for test cases
RETEST_EXPECT_EXT - a file extention for expected results
```
