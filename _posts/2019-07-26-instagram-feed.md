---
layout: post
title:  Create instagram feed
excerpt: Instagram is a simple way to capture and share the world's moments. Follow your friends and family to see what they're up to, and discover accounts from all ...
author: sondh5
categories: [ Other ]
image: "assets/images/instagram_feed.png"
image_hidden: true
featured: false
status: public
---

#### Create new project
```ruby
rails new insta_demo
```

#### Add page controller
Get images from instagram by calling api with `net/http`
```ruby
app/controllers/pages_controller.rb
class PagesController < ApplicationController
  require 'net/http'

  def index
    account_name = params[:account_name] || "arsenal"
    uri = "https://www.instagram.com/#{account_name}/?__a=1"

    result = JSON.parse(Net::HTTP.get(URI.parse(uri)))
    @items = result["graphql"]["user"]["edge_owner_to_timeline_media"]["edges"] rescue []
  end
end
```

#### Update root file
Create route for index page
```ruby
Rails.application.routes.draw do
  root "pages#index"
end
```

#### Add view
```ruby
# app/views/pages/index.html.erb
<div class="container">
  <div class="row">
    <% @items.each do |item| %>
      <%= link_to "https://www.instagram.com/p/#{item["node"]["shortcode"]}", target: "_blank" do %>
        <%= image_tag item["node"]["thumbnail_resources"].last["src"] %>
      <% end %>
    <% end %>
  </div>
</div>

```

Turn on your server
```
rails s
```
and check http://localhost:3000/, it should display 12 recent images.

#### Style your feed
Using bootstrap carousel & font awesome

###### Add jQuery and Bootstrap
```ruby
# app/view/layouts/application.html.erb

<script src="//code.jquery.com/jquery-1.11.1.min.js"></script>
<script src="//maxcdn.bootstrapcdn.com/bootstrap/3.3.0/js/bootstrap.min.js"></script>

<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.0/css/bootstrap.min.css">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">

```

###### Update carousel style
- [index.html](https://github.com/sondh5/insta_demo/blob/master/app/views/pages/index.html.erb)
- [insta_feed.scss](https://github.com/sondh5/insta_demo/blob/master/app/assets/javascripts/carousel.js)
- [carousel.js](https://github.com/sondh5/insta_demo/blob/master/app/assets/javascripts/carousel.js)

###### Enjoy
- Review your result and enjoy


###### Demo
Source code: https://github.com/sondh5/insta_demo <br>
Demo: https://insta-feed-demo.herokuapp.com/ <br>
With other account: <br>>
Eg: https://insta-feed-demo.herokuapp.com/?account_name=vietnam.destinations

