## Custom routes (slugs) and Enums
Date: Dec 29, 2019 2:23 PM

Sections Covered: 66 - 71.

## New Things Learned

### Gem 'friendly_id'

Let's you create human-friendly, pretty URLs to access resources (as opposed to using record IDs). 

github: [https://github.com/norman/friendly_id](https://github.com/norman/friendly_id)

### Enums

ActiveRecord enums allow you to manipulate attributes of an ActiveRecord object such that an attribute's values maps to an integer in the database instead of strings.

To set it up:

- Create a migration to add a new column of type integer to a Model, with the default value as 0

```ruby
    class AddPostStatusToBlogs < ActiveRecord::Migration[5.2]
      def change
        add_column :blogs, :status, :integer, default: 0
      end
    end
```
- Add the enum scope to the Model file

```ruby
    class Blog < ApplicationRecord
      enum status: { draft: 0, published: 1 }
      extend FriendlyId
      friendly_id :title, use: :slugged
    end
```
A cool thing about using enums is you can call the attributes with a `?` and it will return `true` or `false`, for example:

```ruby
2.6.0 :002 > Blog.last.draft?
  Blog Load (0.8ms)  SELECT  "blogs".* FROM "blogs" ORDER BY "blogs"."id" DESC LIMIT $1  [["LIMIT", 1]]
 => false 
2.6.0 :003 > Blog.last.published?
  Blog Load (0.5ms)  SELECT  "blogs".* FROM "blogs" ORDER BY "blogs"."id" DESC LIMIT $1  [["LIMIT", 1]]
 => true 
 ```
