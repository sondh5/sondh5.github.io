---
layout: tils_layout
title: Set basic auth for specific environment
author: sondh5
categories: [ TILs, ruby, rails ]
status: public
---

**For all environment**  
Set authentication in `ApplicationController`
```ruby
# app/controllers/application_controller.rb
class ApplicationController < ActionController::Base
  http_basic_authenticate_with name: 'username', password: 'password'
end
```

**For specific environment**  
Set authentication in `environment.rb`, using rack middleware
```ruby
# config/environments/staging.rb
# also can set for other environment (development, clone, preview...)
Rails.application.configure do
  config.middleware.use Rack::Auth::Basic, "Protected Environment" do |username, password|
    username == "username" && password == "password"
  end
end
```
