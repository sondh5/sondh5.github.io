---
layout: tils_layout
title:  "Boolean type in Rails & Mysql"
author: sondh5
categories: [ TILs, Rails, MySQL ]
status: public
---


`MySQL BOOLEAN data type, which is the synonym of TINYINT(1), value range [-128..127]`

##### Confused situation

| id (integer)        | name (string)           | status (boolean)  |
| ------------- |-------------| -----|
| 1      | Aoi | 1 |
| 2      | Maria      |   10 |

<br>
```ruby
# Rails 4
Idol.find(2).status
=> false

# Rails 5
Idol.find(2).status
=> true
```
##### Explanation

<div class="row">
  <div class="col-md-6 col-sm-12">
  <p>Rails 4 <a href="https://github.com/rails/rails/blob/4-2-stable/activerecord/lib/active_record/type/boolean.rb">boolean.rb</a></p>
  <div class="language-ruby highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">def</span> <span class="nf">cast_value</span><span class="p">(</span><span class="n">value</span><span class="p">)</span>
  <span class="k">if</span> <span class="n">value</span> <span class="o">==</span> <span class="s1">''</span>
    <span class="kp">nil</span>
  <span class="k">elsif</span> <span class="no">TRUE_VALUES</span><span class="p">.</span><span class="nf">include?</span><span class="p">(</span><span class="n">value</span><span class="p">)</span>
    <span class="kp">true</span>
  <span class="k">else</span>
    <span class="c1"># [...]</span>
    <span class="kp">false</span>
  <span class="k">end</span>
<span class="k">end</span>
</code></pre></div></div>

  </div>
  <div class="col-md-6 col-sm-12">
  <p>Rails 5 <a href="https://github.com/rails/rails/blob/5-2-stable/activemodel/lib/active_model/type/boolean.rb">boolean.rb</a></p>
  <div class="language-ruby highlighter-rouge">
    <div class="highlight">
      <pre class="highlight"><code><span class="k">def</span> <span class="nf">cast_value</span><span class="p">(</span><span class="n">value</span><span class="p">)</span>
  <span class="k">if</span> <span class="n">value</span> <span class="o">==</span> <span class="s2">""</span>
    <span class="kp">nil</span>
  <span class="k">else</span>
    <span class="o">!</span><span class="no">FALSE_VALUES</span><span class="p">.</span><span class="nf">include?</span><span class="p">(</span><span class="n">value</span><span class="p">)</span>
  <span class="k">end</span>
<span class="k">end</span>
<br><br>
</code></pre></div></div>
  </div>
</div>
