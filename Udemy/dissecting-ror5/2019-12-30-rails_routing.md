## Rails Routing

### Namespaces
You can organize groups of controllers under a single namespace:
```
namespace :admin do
  get 'dashboard/main'
  get 'dashhboard/user'
  resources :articles
end
```
You have to update the controllers by adding the namespace in the name (such as `Admin::DashboardController` instead of just `DashboardController`). You also have to move the controllers/views into the namespace folders (`app/controllers/admin`). 
