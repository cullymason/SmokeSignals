SmokeSignals
============

A repo that will help ember talk to a php backend (laravel for now)

## The Problem

Ember, specifically Ember-Data, reads and writes JSON in a specific way. Though I wrote it a while ago, here is a gist of what I am trying to solve: [gist](https://gist.github.com/cullymason/6198667)

## My attempt at a solution

The goal would be something like this

```php
  var books = Book::find();
  return Response::ember(books);
```

To achieve this, I would like to implement something similar to rails' Active Model Serializer. I would like to expand the Model by also defining a model serializer. In this serializer you would basically describe how you want your data to be returned for a particular model. And you could have different serializers for different services like Ember.js.

So perhaps it could be something like

```php
  
  class BookSerializer extends EmberSerializer
  {
    $attributes = ['title','number_of_words'];
  
    $relationships = [
      'hasMany'=> ['author','genre'],
      'belongsTo'=> ['barCode']
    ]
  
    $without = ['price'];
    
  }
```
