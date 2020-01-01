## Model Validations, Relationships, Defaults
Date: Jan 01, 2020

Sections Covered: 75 - 79

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

### Relationships
You can use the `add_reference` method to relate one table to another. For example, to relate the `Topic` model to the `Blog` model, we can create a migration like: 
```ruby
class AddTopicReferenceToBlogs < ActiveRecord::Migration[5.2]
  def change
    add_reference :blogs, :topic, foreign_key: true
  end
end
```
A **foreign_key** indicates that an attribute is referencing another table. In this case, the `Blog` model references `Topic` because each blog post will belong to a topic record. 

### Defaults
You can use callbacks (such as `after_initialize`) to set default values in model files.

```ruby
# app/models/portfolio.rb

class Portfolio < ApplicationRecord
  after_initialize :set_defaults

  def set_defaults
    self.main_image ||= "https://place-hold.it/600x400" # the ||= means to apply the value if it doesn't currently exist
    self.thumb_image ||= "https://place-hold.it/350x200" 
  end
end
```
The `||=` operator will apply the operation only if the current value being set is nil. It is basically a shortcut for:
```
if self.main_image == nil
  self.main_image = "value"
end
```
You can also add defaults in migrations like `add_column :blogs, :status, :integer, default: 0`.
