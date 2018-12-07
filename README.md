# No More Explicit process.env

This repository contains some code template that would elaborate you from the dull routine of adding `process.env ||` at the beginning of each Node.js configuration file. Following the [12 Factor's config methodology](https://12factor.net/config), configs are stored in the environment variable, while also be able to read from files for default setting/ bootstrapping, etc.

## Motivation

The motivation of the project are from the [ES6 tutorial](https://github.com/ruanyf/es6tutorial/) and [SmartVIS Back-End](https://github.com/Maecenas/smart-vis-backend) project that I've been doing. I'm excited by the idea of using the ES6's `Proxy`, `Reflect` and `Symbol` feature to introduce an automatic environmental variable loader, without hampering how the rest of code is retrieving configs from file.

```node
// src/app.js
const config = require("../config");
```

## So… What it's like?

We want to keep it this way, and with 50 lines of code, the explicitly annoying `process.env` is now exempted from config implementation.

```node
// FROM: config.js (or config/index.js)
module.exports = {
  env: {
    PORT: process.env.PORT || 3000
  },
  database: {
    HOST: process.env.DATABASE_HOST || "mysql",
    PORT: process.env.DATABASE_PORT || "3306",
    USER: process.env.DATABASE_USER || "example",
    PASSWORD: process.env.DATABASE_PASSWORD || "example",
    DATABASE: process.env.DATABASE_DATABASE || "example"
  }
};
```

```node
// TO: config/default.js
module.exports = {
  env: {
    PORT: 3000
  },
  database: {
    HOST: "mysql",
    PORT: "3306",
    USER: "example",
    PASSWORD: "example",
    DATABASE: "example"
  }
};
```

## Intuition and Installation

But how can we possibly achieve this? The answer is the magical [`config/index.js`](./config/index.js) that I'm going to introduce to you. The intuition is quite clear and straight forward: whenever a client try to get a certain config, we first search for `process.env` and otherwise return the default value (`process.env.KEY || 'default_value'`). An extra key is required for configs of `process.env.SERVICE_FIELD` in order to store the previously called service. ES6's `Proxy`, `Reflect` and `Symbol` feature are required as to intercept the getter. You may check for implementation for more detail.

To get the power of [`no-more-explict-process-env`](https://github.com/Maecenas/no-more-explict-process-env/), just download the [`config/index.js`](./config/index.js) and organized it like the templates, and enjoy!
