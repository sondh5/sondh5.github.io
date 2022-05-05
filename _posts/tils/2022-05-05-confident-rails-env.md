---
layout: tils_layout
title:  Confident Rails ENV
excerpt: This is my way to make sure all environment variables is filled
author: sondh5
categories: [ TILs, Rails ]
status: public
---

##### Problem

Sometimes after deployment my app did not work because of missing ENV

##### Cause

Currently my code look like

```ruby
vault_token = ENV['VAULT_TOKEN']
```

and when I forgot to add `VAULT_TOKEN` to .env file it simple return `nil` so my app failed

##### Solution

Thanks to Confident Ruby and rubocop, I totally move to `fetch`


```ruby
vault_token = ENV.fetch('VAULT_TOKEN')
# => in `fetch': key not found: "VAULT_TOKEN" (KeyError)
```

`fetch` also have options for default value, for block... <br />
FYI: [https://apidock.com/ruby/Hash/fetch](https://apidock.com/ruby/Hash/fetch)
