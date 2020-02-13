---
layout: tils_layout
title: Using Puppeteer in Google Cloud Functions
author: sondh5
categories: [ TILs, Node.js ]
status: public
---

**Setup**
`package.js`
```js
{
  "name": "sample-http",
  "version": "0.0.1",
  "dependencies": {
    "puppeteer": "^1.9.0"
  }
}
```

**Problem**
```js
const browser = await puppeteer.launch();
// Error: Failed to launch chrome!
```
**Solution**
```js
const browser = await puppeteer.launch({
            args: [
                '--no-sandbox',
                '--disable-setuid-sandbox',
            ]
        });
```

Reference to [puppeteerl](https://github.com/puppeteer/puppeteer)
