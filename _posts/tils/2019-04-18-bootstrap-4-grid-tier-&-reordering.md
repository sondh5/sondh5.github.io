---
layout: tils_layout
title:  "Bootstrap 4 grid tier & reordering"
author: sondh5
categories: [ TILs, Bootstrap ]
status: public
---

##### Grid option
From [v4.0.0-alpha.6](https://github.com/twbs/bootstrap/releases/tag/v4.0.0-alpha.6), the `xs` tier no longer requires a breakpoint abbreviation

![bootstrap-v4-grid](/assets/images/tils/bootstrap-v4-grid.png){:height="auto" width="720px"}

##### Reordering
From [v4.0.0-beta](https://github.com/twbs/bootstrap/releases/tag/v4.0.0-beta), use ``.order-`` classes for controlling the visual order of your content

PC view

```
| Column A | Column B |
```

Mobile view
```
| Column B |
| Column A |
```
