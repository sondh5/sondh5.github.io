---
layout: tils_layout
title: Rails Size & Count
author: sondh5
categories: [ TILs, rails ]
status: public
---


Mỗi khi exec query, Active Record sẽ tạo ra biến @loaded = true cho Relation đó.

```ruby
@posts = Post.all

@posts.loaded? #=>true
```

Hàm `size` và `count`
```ruby
def size
  loaded? ? @records.length : count(:all)
end
```

```ruby
def count(column_name = nil, options = {})
  # [...]
  calculate(:count, column_name, options)
end
```
`count` luôn luôn sinh ra query, còn `size` sẽ check relation và query nếu cần.

Rõ ràng là cần cân nhắc dùng `count` để tránh dư thừa query.
