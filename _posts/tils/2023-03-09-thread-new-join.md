---
layout: tils_layout
title:  Thread.new.join
excerpt: Thread.new.join
author: sondh5
categories: [ TILs, Rails ]
status: public
---

```ruby
command = Thread.new do
  # do something
end
command.join
```

The `join` method is used to wait for the thread to complete before continuing with the rest of the program. This ensures that any work performed by the thread has finished before moving on to the next task.
