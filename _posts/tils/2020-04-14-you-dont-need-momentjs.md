---
layout: tils_layout
title: You dont need Momentjs
excerpt: Moment.js is a fantastic time & date library with lots of great features and utilities. However, if you are working on a performance sensitive web application, it might cause a huge performance overhead because of its complex APIs and large bundle size.
author: sondh5
categories: [ TILs, javascript ]
status: public
---


##### Problem

The format I need: `2020-04-20T16:20:00+09:00`

Some code smell I wrote :-ss
```js
const standardizeDate = (date) => {
    date.setHours(date.getHours() + 9);
    return date.toISOString().slice(0, -5) + "+09:00";
}
```


This one looks much better:
```html
<script src="https://unpkg.com/dayjs@1.8.21/dayjs.min.js"></script>
```

```js
const standardizeDate = (date) => dayjs(date).format('YYYY-MM-DDTHH:mm:ssZ');
```

##### Performance concerns


![Large bundle size](https://github.com/you-dont-need/You-Dont-Need-Momentjs/raw/master/screenshot.png)

Shout out to [You-Dont-Need-Momentjs](https://github.com/you-dont-need/You-Dont-Need-Momentjs) and also [dayjs](https://github.com/iamkun/dayjs)
