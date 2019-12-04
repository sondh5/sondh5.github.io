---
layout: tils_layout
title: Better Rails where like query
author: sondh5
categories: [ TILs, SQL, rails ]
status: public
---

**Problem**
```ruby
user_name = "I'm Tony"
User.where("name like '%#{user_name}%'")
# => SELECT  `users`.* FROM `users` WHERE (name like '%I'm Tony%')
=> ActiveRecord::StatementInvalid: Mysql2::Error: You have an error in your SQL syntax;
```

**Better solution**
```ruby
User.where("name like ?", "%#{user_name}%")
# => SELECT  `users`.* FROM `users` WHERE (name like '%I\'m Tony%')
```
