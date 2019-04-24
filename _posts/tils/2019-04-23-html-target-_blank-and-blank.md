---
layout: tils_layout
title: HTML target _blank and blank
author: sondh5
categories: [ TILs, HTML ]
status: public
---

<a href="https://www.w3schools.com/tags/att_a_target.asp" target="_blank"> &lt;a&gt; tag document</a>

```html
<a target="_blank|_self|_parent|_top|framename">
```

- `_blank` always opens url in new window
- `blank` means `framename`, opens url in a window named `blank` if exists, otherwise open new window and name it `blank`
- you possible to set any name for `target` <br>eg: `<a target="new_window">`
