---
layout: memo
title: 日本語のメモ
furigana: true
permalink: /memo
---

<div class="row listrecent">
  {% for category in site.categories %}
    {% if "Memo" == category[0] %}
      <div class="section-title col-md-12 mt-4">
        <h2 id="{{ category[0] | downcase }}">Category <span class="text-capitalize">{{ category[0] }}</span></h2>
      </div>
      {% assign pages_list = category[1] %}
      {% for post in pages_list %}
        {% if post.title != null and post.status == "public" %}
          {% if group == null or group == post.group %}
            <div class="col-lg-6 col-md-6 offset-lg-3 offset-md-3 p-0 card-group article-post memo">
              {% include tilbox.html %}
            </div>
          {% endif %}
        {% endif %}
      {% endfor %}
      {% assign pages_list = nil %}
      {% assign group = nil %}
    {% endif %}
  {% endfor %}
</div>
