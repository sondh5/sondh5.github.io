---
layout: tils_layout
title: Rails cache fetch
author: sondh5
categories: [ TILs, ruby, rails ]
status: public
---

**Problem**  
```ruby
def generate_job_id
  cached_value = Rails.cache.fetch("cache_key", expires_in: 24.hours) do

    job_ids = Job.all.map(&:id) # Trillion jobs

    return [] if job_ids.blank?
    job_ids
  end
  cached_value
end
```

=> Missing cache when job_ids blank, cached_value is nil

```ruby
def generate_job_id
  cached_value = Rails.cache.fetch("cache_key", expires_in: 24.hours) do

    job_ids = Job.all.map(&:id) # Trillion jobs

    break [] if job_ids.blank?
    job_ids
  end
  cached_value
end
```
=> Missing cache when job_ids blank, cached_value is []
```ruby
def generate_job_id
  cached_value = Rails.cache.fetch("cache_key", expires_in: 24.hours) do

    job_ids = Job.all.map(&:id) # Trillion jobs

    job_ids.blank? ? [] : job_ids
  end
  cached_value
end
```
=> Problem solved, "cache_key" 

Reference to
https://github.com/rails/rails/blob/a08a069acdbea8a74282f753a2498d0d7b0c3137/activesupport/lib/active_support/cache.rb#L31
Exactly function
```ruby
#https://github.com/rails/rails/blob/master/activesupport/lib/active_support/cache.rb#L737

def save_block_result_to_cache(name, **options)
  result = instrument(:generate, name, options) do
    yield(name)
  end

  write(name, result, options) unless result.nil? && options[:skip_nil]
  result
end
``` 
The line `write` is not executed => 
