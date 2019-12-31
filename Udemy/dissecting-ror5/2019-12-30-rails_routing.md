## Rails Routing
Date: Dec 30, 2019

Sections Covered: 72 - 74.

### Namespaces
You can organize groups of controllers under a single namespace:
```ruby
# config/routes.rb

Rails.application.routes.draw do
  namespace :admin do
    get 'dashboard/main'
    get 'dashhboard/user'
    resources :articles
  end
 end
```
You have to update the controllers by adding the namespace in the name (such as `Admin::DashboardController` instead of just `DashboardController`). You also have to move the controllers/views into the namespace folders (`app/controllers/admin`). 

### Globbing
Globbing enables you to group items and routes together.

```ruby
# config/routes.rb

Rails.application.routes.draw do
  get 'posts/*missing', to: 'posts#missing'
end
```
The above will route to anything that starts with `posts/`, so all of the following would work: `posts/hello/there`, `posts/i/like/pizza`. The `*` is known as a wildcard segment and it can be placed anywhere in the route you customize. **Note**: The routes file gets compiled from the top down, so be careful if one of your globbed routes comes before another route and results in unexpected behavior.

```ruby
# app/controllers/posts_controller.rb

class PostsController < ApplicationController
  def missing
  end
end
```

```haml
-# app/views/posts/missing.html.haml

%h1 These are not the posts you're looking for
```

### Query String
You can specify dynamic segments that will be available to your controller action when creating a route by  prepending a colon to a fragment:

```ruby
# config/routes.rb

Rails.application.routes.draw do
  get 'query/:random_name', to: 'pages#something'
end

```

```ruby
# app/controllers/pages_controller.rb

class PagesController < ApplicationController
  def something
    @random = params[:random_name]
  end
end
```

```haml
-# app/views/pages/something.html.haml

%h1= @random
```

Rails will treat the attribute with a colon `:` as a dynamic value. The controller action will have the ability to use that attribute passed in.
