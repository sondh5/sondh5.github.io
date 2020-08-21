---
layout: tils_layout
title:  "Spread object support for safari 10 "
excerpt: "Unexpected token '...'. Expected a property name on Safari 10"
author: sondh5
categories: [ TILs, Javascript ]
status: public
---

##### Problem

I got error message "Unexpected token '...'. Expected a property name." when using Safari 10.


##### Cause

Due to  [Document](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Browser_compatibility)
Spread in object literals only support Safari version 11.1 and later.

##### Solution
Using this [plugin](https://babeljs.io/docs/en/babel-plugin-proposal-object-rest-spread) to parse spread to Object assign
```javascript
{
  "plugins": ["@babel/plugin-proposal-object-rest-spread"]
}
```

**In**
```javascript
z = { x, ...y };
```
**Out**
```js
z = Object.assign({ x }, y);
```
