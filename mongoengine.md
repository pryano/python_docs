# MongoEngine #

### Documents and EmbeddedDocuments ###
Documents and EmbeddedDocuments are specified as classes that subclass the Document or EmbeddedDocument classes.
Fields are specified as class variables. Custom fields can be made by subclassing an existing field type.


```python
class Recipe(Document):
  title = StringField(required=True)
  ingredients = EmbeddedDocumentList(Ingredient)


class NameField(StringField):
  pass


class Ingredient(EmbeddedDocument):
  name = NameField(required=True)
  smell = StringField(choices=('good', 'not good', 'not bad', 'bad'))
```
And then we just create it:
```python
r = Recipe(title='Soup', ingredients=[Ingredient(name='water', smell='good')])
r.validate()
r.save()
```

The tricky thing to remember is that a List expects an instance, but EmbeddedDocument or EmbeddedDocumentList expect a callable (a class):
```python
class Man(Document):
  names = List(StringField())
  hairs = EmbeddedDocumentList(Hair)
  # an embeddedDocumentList is just an EmbeddedDocument wrapped in a list.
  same_hairs = List(EmbeddedDocument(Hair))
```

### Validation ###
