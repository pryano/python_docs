# Running Tests #
This will show you how to setup your project for automated tests.
  * Tox: Setup a virtualenv for your tests (can test under multiple python versions)
  * Setup.py: Calls your pytest runner
  * Coverage: Shows how much of your code is covered by your tests

## Setup.py ##
Add the following lines to your setup.py:
``` python
setup_requires=['pytest-runner'],
tests_require=['pytest'],
```
 And create a setup.cfg:
 ``` cfg
 [aliases]
 test=pytest --addopts --verbose
 ```
 
 Now tests can be run by calling `python setup.py test`

## TOX ##
Install tox globally with `pip install tox`

Create a file in your project named `tox.ini`:
``` ini
[tox]
envlist = py34,py35  # Note: you must have the python version on the machine already

[testenv]
deps=
    coverage
commands =
    coverage run setup.py test
    coverage report --omit .*

# next line needs more research    
install_command = pip install --pre --find-links ./shared_resources/bostoolkit/ --no-index {opts} {packages}
```

Call `tox` from the command line or right-click your tox.ini file and select Run to run the tests and coverage report
