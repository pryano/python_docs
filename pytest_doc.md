## Basics ##
```python
def test_uppercase():
    assert 'JIM' == 'jim'.upper()
```

## Expected Exceptions ##
```python
def test_uppercase_wrong_type():
    with pytest.raises(AttributeError):
        x = 10
        x.upper()
```

## Parametrized ##
```python
good_words = ['jim', 'Jim', 'j_m', 'j1m']
expected = ['JIM', 'JIM', 'J_M', 'J1M']

@pytest.parametrized('word, expected', good_words, expected)
def test_uppercase(word, expected):
    assert expected == word.upper()
```

## Basic Fixtures ##
```python
@pytest.fixture
def book():
    Book = collections.namedtuple('Book', 'pages, add_stamp')
    return Book(20, lambda x: True)

def test_library(book):
    assert library.checkout_book(book)
```