---
title: express-note
date: 2020-11-16 23:42:12
tags:
---

# How to solve POST request req.body is empty?

```js
const express = require('express');

const app = express();

app.post('/add', (req, res) =>{
    const {a, b} = req.body; // TypeError: Cannot destructure property 'a' of 'req.body' as it is undefined.
    const ret = parseInt(a) + parseInt(b);
    res.send(`${a} + ${b} = ${ret}`);
});

app.listen(3000, () => {
    console.log(`Example app listening at http://localhost:3000`);
});
```
Install bodyParser to parse body content

1. `npm instll body-parser`
2. Use bodyParser.json and bodyParser.urlencoded as middleware.
```js
const express = require('express');
const bodyParser = require('body-parser')

const app = express();
app.use(bodyParser.urlencoded({ extended:true }));
app.use(bodyParser.json());

app.post('/add', (req, res) =>{
    const {a, b} = req.body; // now you can get your request data here
    const ret = parseInt(a) + parseInt(b);
    res.send(`${a} + ${b} = ${ret}`);
});

app.listen(3000, () => {
    console.log(`Example app listening at http://localhost:3000`);
});
```

