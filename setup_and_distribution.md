# Setup and Distribution #

## Modules and Packages ##
Modules are files ending in .py

Packages are directories that contain an `__init__.py` file and optional modules and packages.


## PIP ##
Two distribution types:
  * source (_source_ distribution)
    * You must compile any cpython dependent code yourself.
    * Contains a setup.py file with build meta information and instructions
    * May contain documentation and tests
  * wheel ( _built_ distribution)
    * If there are dependencies that require cpython compilation, they are already compiled
    * Wheels in pypi usually try to be as general as possible
    * specific to platform, python version, and architecture
    
*For deployments, create a wheel so that everything is precompiled and no downloads are required.*

| command | description |
| --- | --- |
| pip wheel pycrypto  | creates a wheel for you, unless you have a cached version |
| pip wheel --no-cache pycrypto | creates a wheel for you, always |
| pip freeze | creates a requirements.txt file based on the installed packages in your current site-packages/venv |
| pip install -r requirements.txt | install all packages found in the requirements.txt file |

| option | description |
| --- | --- |
| --find-links | use the specified path to find package or wheel |
| --no-index | do not search the online repository for packages |

## Virtual Env ##
  * Isolated python environment.
  * Cheap and easy to create.
  * Prevents package collision where different versions are required for different projects.

  * virtualenvwrapper

| command | description |
| --- | --- |
| lsvirtualenv | list available virtual environments |
| mkvirtualenv my_proj | create a virtual environment |
| mkvirtualenv my_proj -p python3.4 | create a virtual environment with python version 3.4 |
| deactivate | deactivate the current virtual environment |
| workon my_proj | switch to target virtual environment |
| setvirtualenvproject | associate the current directory with a virtual environment |
| rmvirtualenv my_proj | delete the virtual environment |
 
### Pycharm ###
  * Settings
    * project: name
      * project interpreter
        * set interpreter
          * create virtual environment (can tell what python version to use here)
        * view installed packages
        * add packages
  
  You can also specify a virtual environment / interpreter to use in your runconfig for testing different versions.
