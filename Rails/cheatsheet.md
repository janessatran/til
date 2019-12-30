## Cheatsheet for setting up new rails project

### Generators

**Create a new application:** `rails new myrailsapp`. This will create a Rails application called myrailsapp in a directory called `myrailsapp` and install the gem dependecies that are already mentioned in `Gemfile` using `bundle install`. The directory will have a bunch of autogenerated files. You will mostly be working out of the `app` directory. 
**Create a new controller:**: `rails generate controller Welcome index`. This tells rails to create a controller called "Welcome" with an action caled "index". It will create several files, including the controller and view:
- `app/controllers/welcome_controller.rb`
- `app/views/welcome/index.html.erb`

Usually, the `index` action in the controller lists all records in a model. For example, if we had a `UsersController`, the index would list all the users like:

```ruby
class UsersController < ApplicationController
  def index
    @users = User.all
  end
  
end
```
**Creating a model**: `rails generate model User name:string email:string`. This tells rails that we want a `User` model which has a `name` field that is a string, and `email` field which is also a string. Rails responds by creating a bunch of files, including a migration file, which is responsible for creating the database schema later on. 

The available model types in rails include:
*:binary
*:boolean
*:date
*:datetime
*:decimal
*:float
*:integer
*:primary_key
*:string
*:text
*:time
*:timestamp


### Basic tasks
**Setting root (homepage**: To tell rails what to show when we navigate to the root URL of our site, we need to edit the `config/routes.rb` file. This is the application's routing file which holds entries in a special Domain Specific Language (DSL) that tells Rails how to connect incoming requests to controllers and actions. 

Example: 
```ruby
Rails.application.routes.draw do
  get 'welcome/inex'
  
  # tells Rails to map requests to the root of the application 
  # to welcome controller's index action
  root 'welcome#index'
  
end
```
**Starting the server**: run `rails server` or `rails s` for short. 

**Running a migration**: `rails db:migrate`