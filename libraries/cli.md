# Command Line Interfaces
## Complicate Use Case ##
```
book.py [--language LANG] read --page PAGE --paragraph PARA BOOK_NAME
book.py [--language LANG] write (--word WORD_NUM | --page PAGE [--paragraph PARA]) --input INPUT BOOK_NAME
```




### Argparse
This is the built-in library that meets all the use cases I've tried, though it's not as easy to see what all it does at a glance.
```python
parser = ArgumentParser(prog='book.py')
parser.add_argument('--language')
subs = parser.add_subparsers(title='subcommands', dest='subcommand', metavar='(read | write)')
subparsers.required = True
# read
sub_read = subs.add_parser('read')
sub_read.add_argument('--page', required=True)
sub_read.add_argument('--paragraph', required=True)
# write
sub_write = subs.add_parser('write')
sub_write.add_argument('book_name')
sub_write.add_argument('--input')
word_or_page = sub_write.add_mutually_exclusive_group(required=True)
word_or_page.add_argument('--word')
page_and_paragraph = word_or_page.add_argument_group()
page_and_paragraph.add_argument('--page', required=True)
page_and_paragraph.add_argument('--paragraph')
```


### Docopt
This is very readable and covers most use cases. Unfortunately it's no longer maintained.
```python
"""
Usage: book.py
    book.py [--language LANG] read --page PAGE --paragraph PARA BOOK_NAME
    book.py [--language LANG] write (--page PAGE [--paragraph PARA] | --word WORD_NUM) --input INPUT BOOK_NAME

Options:
    BOOK_NAME
    --language LANG
    --page PAGE
    --paragraph PARA
    --word WORD_NUM
    --input INPUT
"""
```


### Python-Fire
https://github.com/google/python-fire

I just found this one and like the simple syntax. I will update this when I have investigated it further.

```python
class Book:
    def __init__(self, language='en'):
        self.language = language
    
    def read(self, book_name, page=None, paragraph=None):
        pass
    
    def write(self, book_name, word=None, page=None, paragraph=None, input=None):
        pass
fire.Fire(Book)
```
