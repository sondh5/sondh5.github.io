---
layout: tils_layout
title: Ruby Array uniq 
author: sondh5
categories: [ TILs, ruby, rails ]
status: public
---

**List post**  
```
post_a (topic_name: "Ruby", priority: 10)  
post_b (topic_name: "PHP", priority: 9)  
post_c (topic_name: "Ruby", priority: 8)  
```

Expect each topic has only 1 post, order by priority

```ruby
current_posts
# => [["Ruby", post_a], ["PHP", post_b], ["Ruby", post_c]]
```

**to_h**
```ruby
current_posts.to_h
# => {"Ruby" => post_c, "PHP" => post_b}
```
=> `post_c` with lower priority is above `post_b` => **ERROR**


**uniq**
```ruby
current_posts.uniq(&:first).to_h
# => {"Ruby" => post_a, "PHP" => post_b}
```
=> as expected
