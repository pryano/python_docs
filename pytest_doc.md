## Basics ##
```python
import pytest

def test_uppercase():
    assert 'JIM' == 'jim'.upper()
```

## Expected Exceptions ##
```python
import pytest

def test_uppercase_wrong_type():
    with pytest.raises(AttributeError):
        x = 10
        x.upper()
```

## Parametrized ##
```python
import pytest

good_words = ['jim', 'Jim', 'j_m', 'j1m']
expected = ['JIM', 'JIM', 'J_M', 'J1M']

@pytest.parametrized('word, expected', good_words, expected)
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

## Mocks ##
Mocks can be used to make dummy objects. You can verify method calls on those objects or just use them so the real (heavier) objects are used.

```python
import pytest
from unittest.mock import Mock

def test_library():
    mock_book = Mock()
    mock_book.add_stamp.return_value = True
    library.checkout_book(mock_book)
    assert mock_book.add_stamp.call_count == 1
```
