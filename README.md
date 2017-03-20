# retick

Redis based task scheduler.

<!--img src='https://raw.githubusercontent.com/evanx/retick/master/docs/readme/images/main.png'-->


## Installation

## Config

See `lib/spec.js` https://github.com/evanx/retick/blob/master/lib/spec.js
```javascript
```

## Implementation

See `lib/main.js` https://github.com/evanx/retick/blob/master/lib/main.js
```javascript
```

### Application archetype

Uses application archetype: https://github.com/evanx/redis-app

See `lib/index.js` https://github.com/evanx/retick/blob/master/lib/index.js
```javascript
require('redis-app')(
    require('../package'),
    require('./spec'),
    async deps => Object.assign(global, deps),
    () => require('./main')
).catch(err => {
    console.error(err);
});
```
where the `config` is extracted from the `spec` defaults and `process.env` overrides. We choose to set `config` et al on `global` before `main` is invoked.


## Docker

See `Dockerfile` https://github.com/evanx/retick/blob/master/Dockerfile
```
FROM mhart/alpine-node:latest
ADD package.json .
RUN npm install --silent
ADD lib lib
ENV NODE_ENV production
CMD ["node", "--harmony", "lib/index.js"]
```

We can build as follows:
```shell
docker build -t retick https://github.com/evanx/retick.git
```
where tagged as image `retick`

<hr>

https://twitter.com/@evanxsummers
