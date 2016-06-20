## Pycharm Setup ##
Pycharm defaults to using unittest as the testrunner. To change it to pytest:

1. In the menu, navigate to File:Settings:Tools:PythonIntegratedTools
2. In the 'Default test runner' field, select 'py.test'
3. Click 'OK' to save the change
4. Select the drop down in the top right of the editor pane, adjacent to the green arrow
5. Select 'Edit configurations...' in the dropdown
6. In the left pane, navigate to Defaults:PythonTests:py.test
7. Check the box to enable the options field and enter '--tb=line' (without quotes)
8. Click 'OK' to save the change

## Basics ##
Pytest will find all test functions that start with test_, and all test classes that start with Test.

```python
import pytest

def test_uppercase():
    assert 'JIM' == 'jim'.upper()
    
def test_uppercase_number():
    assert 'J1M' == 'j1m'.upper(), 'expected number to remain, other letters to be uppercase'
```

## Expected Exceptions ##
```python
import pytest

def test_uppercase_wrong_type():
    with pytest.raises(AttributeError):
        x = 10
        x.upper()
```

## Parametrized Tests##
```python
import pytest

good_words = ['jim', 'Jim', 'j_m', 'j1m']
expected = ['JIM', 'JIM', 'J_M', 'J1M']

@pytest.mark.parametrize('word, expected', zip(good_words, expected))
def test_uppercase(word, expected):
    assert expected == word.upper()
```

## Basic Fixtures ##
```python
import pytest

@pytest.fixture
def book():
    Book = collections.namedtuple('Book', 'pages, add_stamp')
    return Book(20, lambda x: True)

def test_library(book):
    assert library.checkout_book(book)
```

## Setup/Teardown Fixtures ##
Your fixtures can include a teardown method to be called after the test is called:
```python
import pytest

@pytest.fixture
def book(request):                  ## must have request argument
    Book = collections.namedtuple('Book', 'pages, add_stamp')
    def teardown():                 ## define your teardown code
        Book.close()
    request.addfinalizer(teardown)  ## add the teardown method to the request object
    return Book(20, lambda x: True)

def test_library(book):
    assert library.checkout_book(book)
```

## Mocks ##
Mocks can be used to make dummy objects. You can verify method calls on those objects or just use them so the real (heavier) objects are not used.

```python
import pytest
from unittest.mock import Mock

def test_library():
    mock_book = Mock()
    mock_book.add_stamp.return_value = True
    library.checkout_book(mock_book)
    assert mock_book.add_stamp.call_count == 1
```

## MonkeyPatch ##
If you want to change what's returned from an object, but don't have control over the object's creation, you can monkeypatch the method you want to change.
```python
import pytest
@pytest.fixture
def no_db(monkeypatch):
    monkeypatch.setattr(library.dbservice.BookService, 'find_all_books', lambda: {'Book A': {'pages': 90}})

def test_library(no_db):
    books = library.show_books()   # behind the scenes this calls BookService.find_all_books()
    assert books == {'Book A': {'pages': 90}}
```
