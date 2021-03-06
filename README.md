# Active Record Lite

Active Record Lite is an Object Relational Mapper built following the Active
Record architectural pattern, particularly the implementation found in Ruby
on Rails. Active Record Lite is a streamlined means by which to model and
associate database tables. For a demonstration, download the repo and run `rake demo_console`, from the root folder. The demo schema has a table of lists and a table of todos in a one to many relationship.



[URL Shortener](http://www.lync.space/) is an app deployed to Heroku that uses a modified version of this active record implementation to interact with a PostgreSQL DB.

## SQLObject

This is the model class. Basic usage is as follows.
```ruby
class Todo < SQLObject
  self.finalize!
end
```
### Methods
```ruby
Todo.all
```
Returns all table rows.

```ruby
Todo.where(column: value)
```
Returns all table rows that match the inserted parameters, via Searchable module.

```ruby
Todo.find(id)
```
Returns the table row with the corresponding id.

```ruby
@todo = Todo.new(name: 'Clean Bedroom')
@todo.save
```
Saves object as row to corresponding table or, if an id is already present, updates the row with the corresponding id.

## Associatable

Associatable is a module that allows table object associations. Basic usage is as follows.
```ruby
class Todo < SQLObject
  belongs_to(
    :list,
    class_name: 'List',
    foreign_key: :list_id,
    primary_key: :id
  )
  self.finalize!
end
```
If `:class_name`,`:foreign_key` or `:primary_key` are left empty, they will be auto populated with default values that following the naming conventions in Ruby on Rails. The following would also be valid.
```ruby
class Todo < SQLObject
  belongs_to :list
  self.finalize!
end
```
