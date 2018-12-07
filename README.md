# No More Explicit process.env

This repository contains some code template that would elaborate you from the dull routine of adding `process.env ||` at the beginning of each Node.js configuration file. Following the [12 Factor's config methodology](https://12factor.net/config), configs are stored in the environment variable, while also be able to read from files for default setting/ bootstrapping, etc.

