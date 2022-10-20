---
layout: tils_layout
title:  Devise paranoid
excerpt: For security and privacy, hide email not found message
author: sondh5
categories: [ TILs, Rails ]
status: public
---

##### Problem

When trying to reset password with not exists email => "Email not found"

##### Cause

Normal action of devise but not good if someone want to know your user email

##### Solution

Use devise paranoid mode

```ruby
# It will change confirmation, password recovery and other workflows
# to behave the same regardless if the e-mail provided was right or wrong.
# Does not affect registerable.
config.paranoid = true
```
