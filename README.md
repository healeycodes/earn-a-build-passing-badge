[![Build Status](https://travis-ci.com/healeycodes/earn-a-build-passing-badge.svg?branch=master)](https://travis-ci.com/healeycodes/earn-a-build-passing-badge)

### Earn a Build Passing Badge on GitHub ✅! Testing Your Express App with Travis CI

<br>

This repo contains the are the files for my tutorial on continuous intregration with Jest, Express, and Travis CI.

It also serves as a live example! Whenever there is a commit to `master`, Travis CI will queue up a new test build.

The result of that build will affect the Build Status badge you see at the top there. If the build fails, I will get an email too.

<br>

`npm i` will install all of the dependencies. The rest of the application — how to run and test it — is explained below.

<br>

#### app.js

This contains our application routes and logic.

```javascript
const express = require('express');
const app = express();

app.get('/', async (req, res) => res.status(200).send('Hello World!'));

module.exports = app;
```

<br>

#### server.js

`npm start` will run this file, running the application.

```javascript
const app = require('./app');
const port = 3000;

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

<br>

#### app.test.js

Here are our tests for Jest to run when `npm test` is called.

```javascript
const app = require('../app');
const request = require('supertest');

describe('GET /', () => {
    it('responds with 200', async () => {
        await request(app)
            .get('/')
            .expect(200);
    });
})
```

<br>

#### .travis.yml

This file tells Travis CI [how to setup testing](https://docs.travis-ci.com/user/customizing-the-build/) for the repository. Make sure you've installed Travis CI as a GitHub App and toggled on repository permissions.

```yml
language: node_js
node_js:
- lts/*
```
