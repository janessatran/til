## Model Validations and Relationships
Date: Jan 01, 2020

Sections Covered: 75 - 

### Validations
To ensure that a column is never null in a table, you can use `validates_presence_of`:
```ruby
# app/models/blog.rb

class Blog < ApplicationRecord
  enum status: { draft: 0, published: 1 }
  extend FriendlyId
  friendly_id :title, use: :slugged

  validates_presence_of :title, :body
end
```
This ensures that every time a new record is created in the Blog table, it must have a `title` and `body` in order to be saved to the DB.

### Data Relationships
You can use the `add_reference` method to relate one table to another. For example, to relate the `Topic` model to the `Blog` model, we can create a migration like: 
```ruby
class AddTopicReferenceToBlogs < ActiveRecord::Migration[5.2]
  def change
    add_reference :blogs, :topic, foreign_key: true
  end
end
```
A **foreign_key** indicates that an attribute is referencing another table. In this case, the `Blog` model references `Topic` because each blog post will belong to a topic record. 
