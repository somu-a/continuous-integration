# Continuous Integration ![https://github.com/somu-a/continuous-integration/actions?query=workflow%3Atests](https://github.com/somu-a/continuous-integration/workflows/tests/badge.svg)

*This is the first homework assignment for [Claremont McKenna's CSCI46: Data Structures](https://github.com/mikeizbicki/cmc-csci046) course.*

Continuous Integration (CI) is a technique for proving that your code is correct.
CI tools run your code's test cases automatically when you commit code to your repo,
and let you know if anything is broken.

In this class, we will be using GitHub Actions for CI.
It is a standard tool used by many open source applications in order to maintain code quality.
Whenever you submit a pull request to an open source project,
it will have to pass the CI tests in order for the maintainer to accept your changes.
This process ensures that thousands of developers can work together on the same project without breaking each other's code.

All of your homework grades in this class will be determined by the results of the CI tests.
If you pass all the tests, you get full credit.
For each test case that you fail, you will lose 1 point on the assignment.

The workflow is summarized in the following diagram:

<p align=center>
<img src=diagram.png?raw=true width=500px>
</p>

In this assignment, you will create a sample project that uses CI to run some simple tests.
There is very little coding in this assignment, and the purpose is to ensure that you understand the mechanics of how to get CI running correctly.

## Instructions

Fork this repo, and clone your fork onto the lambda server.

`cd` into your cloned repo and run the `ls -a` command.
You should see many files as described in the following table.

| file | purpose |
| ---- | --- |
| `.`    | special system file that refers to the current folder |
| `..`   | special system file that refers to the previous folder |
| `.git` | contains all the information about the git repo; it is created when running `git init` and should never be modified directly |
| `.github` | contains the instructions for the CI tests; you will not need to edit these files for this class, but you can see https://docs.github.com/en/actions for more info |
| `.gitignore` | tells git which files should not be added into the repo; you will not need to edit these files for this class, but you can see https://git-scm.com/docs/gitignore for more info |
| `README.md` | contains the description of the project your currently reading |
| `Fixme.py` | contains the project's python code that you will have to fix |

### Running the test cases

This project uses the `doctest` module for its test cases.
`doctest` is a standard python module that comes with every python installation.
In order to run the doctests, execute the command
```
$ python3 -m doctest Fixme.py
```
You should get output similar to
```
**********************************************************************
File "/home/user/proj/cmc-csci046/week_00/homework/Fixme.py", line 32, in Fixme.triangular
Failed example:
    triangular(1)
Expected:
    1
Got nothing
**********************************************************************
File "/home/user/proj/cmc-csci046/week_00/homework/Fixme.py", line 34, in Fixme.triangular
Failed example:
    triangular(2)
Expected:
    3
Got nothing
**********************************************************************
File "/home/user/proj/cmc-csci046/week_00/homework/Fixme.py", line 36, in Fixme.triangular
Failed example:
    triangular(3)
Expected:
    6
Got nothing
**********************************************************************
File "/home/user/proj/cmc-csci046/week_00/homework/Fixme.py", line 38, in Fixme.triangular
Failed example:
    triangular(4)
Expected:
    10
Got nothing
**********************************************************************
File "/home/user/proj/cmc-csci046/week_00/homework/Fixme.py", line 40, in Fixme.triangular
Failed example:
    triangular(40)
Expected:
    820
Got nothing
**********************************************************************
File "/home/user/proj/cmc-csci046/week_00/homework/Fixme.py", line 42, in Fixme.triangular
Failed example:
    triangular(400)
Expected:
    80200
Got nothing
**********************************************************************
1 items had failures:
   6 of   6 in Fixme.triangular
***Test Failed*** 6 failures.
```
This message tells us that there are currently 6 failing test cases.

Fix these test cases by editing the python file `Fixme.py` so that the function `triangular` is implemented.
This should be really easy: just copy the code from the `factorial` function, but replace the `*` with `+`.

Once you've made your changes, rerun the doctest command
```
$ python3 -m doctest Fixme.py
```
If everything is working correctly,
then the command should have no output.
This means that you are passing all the tests.

**NOTE:**
On all your assignments in this class,
you will lost 1 point for each test case that is not passing.

### Running the linter

A *linter* is a program that enforces style constraints on code.
When many programmers collaborate on a project,
it becomes much easier if they all use the same style.

For example, how to name variables is a common style issue.
Some programmers use what's called camel case to name variables.
For example, `thisVariableIsCamelCase` because the capital letters are the "humps" of the camel.
Python, however, is a snake, so python programmers use snake case:
`this_variable_is_snake_case` because the underscores are "snakes" connecting the letters.
It's not technically wrong to use camel case in your python code,
but it makes it harder for other programmers to understand your code.

Python has a large set of these style rules that "true" python programmers follow.
These rules are codified in [PEP8](https://www.python.org/dev/peps/pep-0008/),
which was introduced by Python's [Benevolent Dictator For Life (BDFL)](https://en.wikipedia.org/wiki/Benevolent_dictator_for_life) [Guido van Rossum](https://gvanrossum.github.io/).
PEP stands for Python Enhancement Proposal, and it's the 8th such proposal that's been accepted.
There are currently [hundreds of PEPs](https://www.python.org/dev/peps/) that address different aspects of python.
It is common for people to talk about PEP8, so you must know what that is, but you don't need to know any of the others.

In this class, we will be enforcing that all of your code satisfies PEP8 using a python linter called `flake`.
To lint your program, type the command
```
$ flake8 Fixme.py
```
You should get output similar to
```
Fixme.py:20:11: E225 missing whitespace around operator
Fixme.py:21:21: E231 missing whitespace after ','
Fixme.py:22:15: E225 missing whitespace around operator
Fixme.py:25:1: E302 expected 2 blank lines, found 1
```
which tells you all of the linting errors your code has.
Fix your code so that `flake8` reports no linting errors on your code.

**NOTE:**
The CI tests first run the linter, then run the doctests.
If the linter fails, then no doctests will run, and you will get a 0 on your assignment.
You should infer from this that learning good pythonic programming style is a very important part of your grade in this class.

### Using CI

Now that you've made changes to your code, you should commit those changes and push them to github.
Recall that this is done with the commands
```
$ git add Fixme.py
$ git commit
$ git push origin master
```
As soon as you run the push command, github will automatically start running your code against 4 different versions of python (versions 3.6, 3.7, 3.8, and 3.9).
Click the "actions" button at the top of your forked project webpage to see the results.

You should see 4 green "builds" indicating that your program passed all test cases for each python version tested.
If you see any red builds, then something went wrong, and you need to fix that problem before continuing.

### The CI badge

Most repos that use CI place a *badge* in their README file that indicatees the status of the most recent build.
A green badge demonstrates that the repo passes all test cases,
and therefore should instill confidence in potential users of the software that the software is high quality.

This repo's `README.md` file already contains a badge,
but that badge is currently red even though you pass all your test cases.
The problem is that because you forked from my repo,
the badge is still pointing to my repo instead of yours.
In particular,
the first line of the file currently contains the text

```
# Continuous Integration ![https://github.com/mikeizbicki/continuous-integration/actions?query=workflow%3Atests](https://github.com/mikeizbicki/continuous-integration/workflows/tests/badge.svg)
```

To fix this problem and get the correct badge,
you need to modify the `README.md` so that the URL contains your username instead of `mikeizbicki`.
After doing so, add the file to git, commit the file, and push your changes to github.

Now view your forked repo in your web browser.
You should see a green badge instead of a red badge if you made all of the changes correctly.

**NOTE:**
Whenever the grader sees a green badge on your homework submissions,
it guarantees full credit on the assignment.

## Submission

To submit this assignment, you will past the URL to your github repo into sakai.
The URL should be of the format
```
https://github.com/mikeizbicki/continuous-integration
```
but with your github username instead of mine.

**IMPORTANT:**
It is not enough in this class to simply push your final code onto github.
The grader will not know to grade your code unless you also submit it into sakai.
