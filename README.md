

![repo-banner](https://user-images.githubusercontent.com/4060187/28923990-050a32d4-782e-11e7-9da7-574ce5a8b455.png)

[![CircleCI](https://circleci.com/gh/jaredpalmer/razzle/tree/master.svg?style=shield)](https://circleci.com/gh/jaredpalmer/razzle/tree/master) ![Razzle-status](https://david-dm.org/jaredpalmer/razzle.svg?path=packages/razzle) [![npm version](https://badge.fury.io/js/razzle.svg)](https://badge.fury.io/js/razzle) [![Known Vulnerabilities](https://snyk.io/test/npm/razzle/badge.svg)](https://snyk.io/test/npm/razzle) [![Greenkeeper badge](https://badges.greenkeeper.io/jaredpalmer/razzle.svg)](https://greenkeeper.io/) [![Join the community on Spectrum](https://withspectrum.github.io/badge/badge.svg)](https://spectrum.chat/palmer)

Universal JavaScript applications are tough to setup. Either you buy into a framework like [Next.js](https://github.com/zeit/next.js) or [react-server](https://github.com/redfin/react-server), fork a boilerplate, or set things up yourself. Aiming to fill this void, Razzle is a tool that abstracts all complex configuration needed for SSR into a single dependency--giving you the awesome developer experience of [create-react-app](https://github.com/facebookincubator/create-react-app), but then leaving the rest of your app's architectural decisions about frameworks, routing, and data fetching up to you. With this approach, Razzle not only works with React, but also Reason, Elm, Vue, Angular, and most importantly......whatever comes next.

**Razzle comes with the "battery-pack included"**:

- :fire: Universal Hot Module Replacement, so both the client and server update whenever you make edits. No annoying restarts necessary
- Comes with your favorite ES6 JavaScript goodies (through `babel-preset-razzle`)
- Comes with the same CSS setup as [create-react-app](https://github.com/facebookincubator/create-react-app)
- Works with [React](https://github.com/facebook/react), [Preact](https://github.com/developit/preact), [Elm](http://elm-lang.org/), [Reason-React](https://github.com/jaredpalmer/razzle/tree/master/examples/with-reason-react), [Inferno](https://github.com/infernojs), and [Rax](https://github.com/alibaba/rax) as well as [Angular](https://github.com/angular/angular) and [Vue](https://github.com/vuejs/vue) if that's your thing
- Escape hatches for customization via `.babelrc` and `razzle.config.js`
- [Jest](https://github.com/facebook/jest) test runner setup with sensible defaults via `razzle test`
- :rocket: SPA mode, build client side apps with razzle

## Quick Start

```bash
npx create-razzle-app my-app
cd my-app
npm start
```

Then open http://localhost:3000/ to see your app. Your console should look like this:

<img src="https://cloud.githubusercontent.com/assets/4060187/26324663/b31788c4-3f01-11e7-8e6f-ffa48533af54.png" width="500px" alt="Razzle Development Mode"/>

**That's it**. You don't need to worry about setting up multiple webpack configs or other build tools. Just start editing `src/App.js` and go!

Below is a list of commands you will probably find useful.

### `npm start` or `yarn start`

Runs the project in development mode.  
You can view your application at `http://localhost:3000`

The page will reload if you make edits.

### `npm run build` or `yarn build`

Builds the app for production to the build folder.

The build is minified and the filenames include the hashes.
Your app is ready to be deployed!

### `npm run start:prod` or `yarn start:prod`

Runs the compiled app in production.

You can again view your application at `http://localhost:3000`

### `npm prerender` or `yarn prerender`

Renders a static version of specified routes to the build folder based on the built production app.
See [Experimental](#experimental) on how to enable prerender.
Your prerendered app is ready to be served!

### `npm test` or `yarn test`

Runs the test watcher (Jest) in an interactive mode.
By default, runs tests related to files changed since the last commit.

### `npm start -- --inspect=[host:port]` or `yarn start -- --inspect=[host:port]`

To debug the node server, you can use `razzle start --inspect`. This will start the node server and enable the inspector agent. The `=[host:port]` is optional and defaults to `=127.0.0.1:9229`. For more information, see [this](https://nodejs.org/en/docs/guides/debugging-getting-started/).

### `npm start -- --inspect-brk=[host:port]` or `yarn start -- --inspect-brk=[host:port]`

This is the same as --inspect, but will also break before user code starts. (to give a debugger time to attach before early code runs) For more information, see [this](https://nodejs.org/en/docs/guides/debugging-getting-started/).

### `rs`

If your application is running, and you need to manually restart your server, you do not need to completely kill and rebundle your application. Instead you can just type `rs` and press enter in terminal.

## <img src="https://user-images.githubusercontent.com/4060187/37915268-209644d0-30e7-11e8-8ef7-086b529ede8c.png" width="500px" alt="Razzle Hot Restart"/>

<!-- INSERT doctoc generated TOC please keep comment here to allow auto update -->
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Quick Start](#quick-start)
  - [`npm start` or `yarn start`](#npm-start-or-yarn-start)
  - [`npm run build` or `yarn build`](#npm-run-build-or-yarn-build)
  - [`npm run start:prod` or `yarn start:prod`](#npm-run-startprod-or-yarn-startprod)
  - [`npm test` or `yarn test`](#npm-test-or-yarn-test)
  - [`npm start -- --inspect=[host:port]` or `yarn start -- --inspect=[host:port]`](#npm-start------inspecthostport-or-yarn-start------inspecthostport)
  - [`npm start -- --inspect-brk=[host:port]` or `yarn start -- --inspect-brk=[host:port]`](#npm-start------inspect-brkhostport-or-yarn-start------inspect-brkhostport)
  - [`rs`](#rs)
- [<img src="https://user-images.githubusercontent.com/4060187/37915268-209644d0-30e7-11e8-8ef7-086b529ede8c.png" width="500px" alt="Razzle Hot Restart"/>](#img-srchttpsuser-imagesgithubusercontentcom406018737915268-209644d0-30e7-11e8-8ef7-086b529ede8cpng-width500px-altrazzle-hot-restart)
- [Customization](#customization)
  - [Plugins](#plugins)
    - [Using Plugins](#using-plugins)
    - [Writing Plugins](#writing-plugins)
  - [Customizing Babel Config](#customizing-babel-config)
  - [Extending Webpack](#extending-webpack)
  - [CSS Modules](#css-modules)
  - [Polyfills](#polyfills)
- [Environment Variables](#environment-variables)
  - [Build-time Variables](#build-time-variables)
  - [Runtime Variables](#runtime-variables)
  - [Adding Temporary Environment Variables In Your Shell](#adding-temporary-environment-variables-in-your-shell)
    - [Windows (cmd.exe)](#windows-cmdexe)
    - [Linux, macOS (Bash)](#linux-macos-bash)
  - [Adding Environment Variables In `.env`](#adding-environment-variables-in-env)
  - [Expanding Environment Variables In `.env`](#expanding-environment-variables-in-env)
    - [What other `.env` files are can be used?](#what-other-env-files-are-can-be-used)
- [How Razzle works (the secret sauce)](#how-razzle-works-the-secret-sauce)
- [Inspiration](#inspiration)
    - [Author](#author)
- [Contributors](#contributors)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Build Types

In addition to universal/isomorphic appplications, Razzle can build single page (or client-only) applications. To do this, you can remove `index.js` and `server.js` then add `index.html` file inside public folder, at the end pass `--type=spa` to your `package.json`'s scripts like so:

```diff
"scripts": {
-  "start": "razzle start",
+  "start": "razzle start --type=spa",
-  "build": "razzle build",
+  "build": "razzle build --type=spa",
  "test": "razzle test --env=jsdom",
-  "start:prod": "NODE_ENV=production node build/server.js"
+  "start:prod": "serve -s build/public"
}
```

## Customization

### Plugins

As of Razzle 2.0, you can add your plugins to modify your setup.

- [TypeScript](https://github.com/jaredpalmer/razzle/tree/master/packages/razzle-plugin-typescript)
- [Vue](https://github.com/jaredpalmer/razzle/tree/master/packages/razzle-plugin-vue)
- [Elm](https://github.com/jaredpalmer/razzle/tree/master/packages/razzle-plugin-elm)
- [MDX](https://github.com/jaredpalmer/razzle/tree/master/packages/razzle-plugin-mdx)
- [See All](https://www.npmjs.com/search?q=razzle-plugin)

#### Using Plugins

You can use Razzle plugins by installing in your project and adding them to your `razzle.config.js`. See the README.md of the specific plugin, but generally speaking, the flow is something like...

```bash
yarn add razzle-plugin-xxxx
```

```js
//./razzle.config.js
module.exports = {
  plugins: ['xxxx'],
};
```

#### Writing Plugins

Plugins are simply functions that modify and return Razzle's webpack config.

```js
'use strict';

module.exports = function myRazzlePlugin(webpackConfig, env, webpack, options) {
  const { target, dev } = env;

  if (target === 'web') {
    // client only
  }

  if (target === 'server') {
    // server only
  }

  if (dev) {
    // dev only
  } else {
    // prod only
  }

  // Do some stuff...
  return webpackConfig;
};
```

##### New in razzle 3.2

Plugins also support using promises

```js
'use strict';

module.exports = function myRazzlePlugin(webpackConfig, env, webpack, options) {
  const { target, dev } = env;

  return new Promise(async (resolve) => {
    if (target === 'web') {
      // client only
    }

    if (target === 'server') {
      // server only
    }

    if (dev) {
      // dev only
      await getDevcert();
    } else {
      // prod only
    }

    // Do some stuff...
    resolve(webpackConfig);
  })
};
```

### Customizing Babel Config

Razzle comes with most of ES6 stuff you need. However, if you want to add your own babel transformations, just add a `.babelrc` file to the root of your project.

```js
{
  "presets": [
    "razzle/babel", // NEEDED
    "stage-0"
   ],
   "plugins": [
     // additional plugins
   ]
}
```

A word of advice: the `.babelrc` file will replace the internal razzle babelrc template. You must include at the very minimum the default razzle/babel preset.

### Extending Webpack

You can also extend the underlying webpack config. Create a file called `razzle.config.js` in your project's root.

```js
// razzle.config.js

module.exports = {
  modify: (config, { target, dev }, webpack) => {
    // do something to config

    return config;
  },
};
```

A word of advice: `razzle.config.js` is an escape hatch. However, since it's just JavaScript, you can and should publish your `modify` function to npm to make it reusable across your projects. For example, imagine you added some custom webpack loaders and published it as a package to npm as `my-razzle-modifictions`. You could then write your `razzle.config.js` like so:

```
// razzle.config.js
const modify = require('my-razzle-modifictions');

module.exports = {
  modify
}
```

Last but not least, if you find yourself needing a more customized setup, Razzle is _very_ forkable. There is one webpack configuration factory that is 300 lines of code, and 4 scripts (`build`, `start`, `test`, and `init`). The paths setup is shamelessly taken from [create-react-app](https://github.com/facebookincubator/create-react-app), and the rest of the code related to logging.


#### New in razzle 3.2

`razzle.config.js` modify also support using promises

```js
// razzle.config.js

module.exports = {
  modify: (webpackConfig, { target, dev }, webpack) => {

    return new Promise(async (resolve) => {
      if (target === 'web') {
        // client only
      }

      if (target === 'server') {
        // server only
      }

      if (dev) {
        // dev only
        await getDevcert();
      } else {
        // prod only
      }

      // Do some stuff...
      resolve(webpackConfig);
    })
  },
};
```

### CSS Modules

Razzle supports [CSS Modules](https://github.com/css-modules/css-modules) using Webpack's [css-loader](https://github.com/webpack-contrib/css-loader). Simply import your CSS file with the extension `.module.css` and Razzle will process the file using `css-loader`.

```jsx
import React from 'react';
import styles from './style.module.css';

const Component = () => <div className={styles.className} />;

export default Component;
```

### Polyfills

Polyfills for IE 9, IE 10, and IE 11 are no longer included by default (but you can opt in!)
We have dropped default support for Internet Explorer 9, 10, and 11. If you still need to support these browsers, follow the instructions below.

First, install `react-app-polyfill`:

`npm install react-app-polyfill`
or

`yarn add react-app-polyfill`
Next, place one of the following lines at the very top of `src/client.js:`

```javascript
import 'react-app-polyfill/ie9'; // For IE 9-11 support
import 'react-app-polyfill/ie11'; // For IE 11 support
```

### Experimental

Razzle has support for some experimental features. Currently razzle has experimental support for [react-refresh](https://github.com/pmmmwh/react-refresh-webpack-plugin) and prerender. More features may be added in the future and may become fully supported features.

To enable react-refresh:

```js
// razzle.config.js

module.exports = {
  experimental: {
    reactRefresh: true,
  },
};
```

To enable prerender:

Add `prerender` to your `package.json`'s scripts like so:

```diff
"scripts": {
+  "prerender": "razzle prerender --routes=routes.json",
}
```

Add a `routes.json` to your app dir:

```json
["/","/about"]
```

Add a `experimental.prerender` to your `razzle.config.js`:

```js
// razzle.config.js

module.exports = {
  experimental: {
    prerender: true,
  },
};
```

To enable prerender with options:

```js
// razzle.config.js

module.exports = {
  experimental: {
    prerender: {
      entrypoint: 'server.js',
      export: 'render'
    },
  },
};
```

## Environment Variables

### Build-time Variables

**The following environment variables are embedded during the build time.**

* `process.env.RAZZLE_PUBLIC_DIR`: Absolute path to the public directory in the server's filesystem.
* `process.env.RAZZLE_CHUNKS_MANIFEST`: Path to a file containing compiled chunk outputs
* `process.env.RAZZLE_ASSETS_MANIFEST`: Path to a file containing compiled asset outputs
* `process.env.REACT_BUNDLE_PATH`: Relative path to where React will be bundled during development. Unless you are modifying the output path of your webpack config, you can safely ignore this. This path is used by `react-error-overlay` and webpack to power up the fancy runtime error iframe. For example, if you are using common chunks and an extra entry to create a vendor bundle with stuff like react, react-dom, react-router, etc. called `vendor.js`, and you've changed webpack's output to `[name].js` in development, you'd want to set this environment variable to `/static/js/vendor.js`. If you do not make this change, nothing bad will happen, you will simply not get the cool error overlay when there are runtime errors. You'll just see them in the console. Note: This does not impact production bundling.
* `process.env.VERBOSE`: default is false, setting this to true will not clear the console when you make edits in development (useful for debugging).
* `process.env.PORT`: The `BUILD_TARGET=server` build listens on this port for all NODE_ENVs. default is `3000`
* `process.env.HOST`: The IP address that the server will bind to. default is `0.0.0.0`, for INADDR_ANY
* `process.env.NODE_ENV`: `'development'` or `'production'`
* `process.env.BUILD_TYPE`: `'iso'` for isomorphic/universal applications or `'spa'` for single page applications. The default is `'iso'`. This is set by CLI arguments.
* `process.env.BUILD_TARGET`: either `'client'` or `'server'`
* `process.env.PUBLIC_PATH`: Only used in `razzle build`. You can alter the `webpack.config.output.publicPath` of the client assets (bundle, css, and images). This is useful if you plan to serve your assets from a CDN. Make sure to _include_ a trailing slash (e.g. `PUBLIC_PATH=https://cdn.example.com/`). If you are using React and altering the public path, make sure to also [include the `crossorigin` attribute](https://reactjs.org/docs/cdn-links.html#why-the-crossorigin-attribute) on your `<script>` tag in `src/server.js`.
* `process.env.CLIENT_PUBLIC_PATH`: The `NODE_ENV=development` build's `BUILD_TARGET=client` has a different `PUBLIC_PATH` than `BUILD_TARGET=server`. Default is `http://${process.env.HOST}:${process.env.PORT + 1}/`

You can create your own custom environment variables that will be inlined during the build. They must start
with `RAZZLE_`. Any other variables except the ones listed above will be ignored to avoid accidentally exposing a private key on the machine that could have the same name. Changing any environment variables will require you to restart the development server if it is running.

These environment variables will be defined for you on `process.env`. For example, having an environment variable named `RAZZLE_SECRET_CODE` will be exposed in your JS as `process.env.RAZZLE_SECRET_CODE`.

### Runtime Variables

Using the dotenv package, or by defining variables in your shell (see below), you can get access to runtime environment variables. This is useful for services like Heroku which dynamically set `process.env.PORT` for example. Be careful when referencing runtime variables in isomorphic code as they will be `undefined` in the browser, but defined when running in Node. This can lead to weird behavior. If you need to make runtime variables available to the browser, it is up to you to deliver them. You can stringify them and place them on `window`...

```js
// config.js
export const runtimeConfig =
  typeof window !== 'undefined'
    ? {
        // client
        myThing: window.env.myThing,
        anotherThing: window.env.anotherThing,
      }
    : {
        // server
        myThing: process.env.MY_THING,
        anotherThing: process.env.ANOTHER_THING,
      };
```

Now we set `window.env` as `runtimeConfig` when we go to render the HTML.

```js
import App from './App';
import React from 'react';
import express from 'express';
import { renderToString } from 'react-dom/server';
import serialize from 'serialize-javascript'; // Safer stringify, prevents XSS attacks
import { runtimeConfig } from './config';
const chunks = require(process.env.RAZZLE_CHUNKS_MANIFEST);

const server = express();

server
  .disable('x-powered-by')
  .use(express.static(process.env.RAZZLE_PUBLIC_DIR))
  .get('/*', (req, res) => {
    const markup = renderToString(<App />);
    res.send(
      // prettier-ignore
      `<!doctype html>
    <html lang="">
    <head>
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta charSet='utf-8' />
        <title>Welcome to Razzle</title>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        ${chunks.client.css.map(path => `<link rel="stylesheet" href="${path}">`)}
    </head>
    <body>
        <div id="root">${markup}</div>
        <script>window.env = ${serialize(runtimeConfig)};</script>
        ${chunks.client.js.map(path => `<script src="${path}" defer crossorigin></script>`)}        
    </body>
</html>`
    );
  });

export default server;
```

### Adding Temporary Environment Variables In Your Shell

Defining environment variables can vary between OSes. It’s also important to know that this manner is temporary for the
life of the shell session.

#### Windows (cmd.exe)

```cmd
set RAZZLE_SECRET_CODE=abcdef&&npm start
```

(Note: the lack of whitespace is intentional.)

#### Linux, macOS (Bash)

```bash
RAZZLE_SECRET_CODE=abcdef npm start
```

### Adding Environment Variables In `.env`

To define permanent environment variables, create a file called .env in the root of your project:

```
RAZZLE_SECRET_CODE=abcdef
```

### Expanding Environment Variables In `.env`

Expand variables already on your machine for use in your `.env` file.

For example, to get the environment variable `npm_package_version`:

```
RAZZLE_VERSION=$npm_package_version
# also works:
# RAZZLE_VERSION=${npm_package_version}
```

Or expand variables local to the current `.env` file:

```
DOMAIN=www.example.com
RAZZLE_FOO=$DOMAIN/foo
RAZZLE_BAR=$DOMAIN/bar
```

#### What other `.env` files are can be used?

- `.env`: Default.
- `.env.local`: Local overrides. **This file is loaded for all environments except test.**
- `.env.development`, `.env.test`, `.env.production`: Environment-specific settings.
- `.env.development.local`, `.env.test.local`, `.env.production.local`: Local overrides of environment-specific settings.

Files on the left have more priority than files on the right:

- `npm start`: `.env.development.local`, `.env.development`, `.env.local`, `.env`
- `npm run build`: `.env.production.local`, `.env.production`, `.env.local`, `.env`
- `npm test`: `.env.test.local`, `.env.test`, `.env` (note `.env.local` is missing)

These variables will act as the defaults if the machine does not explicitly set them.<br>
Please refer to the [dotenv documentation](https://github.com/motdotla/dotenv) for more details.

> Note: If you are defining environment variables for development, your CI and/or hosting platform will most likely need
> these defined as well. Consult their documentation how to do this. For example, see the documentation for [Travis CI](https://docs.travis-ci.com/user/environment-variables/) or [Heroku](https://devcenter.heroku.com/articles/config-vars).

## create-razzle-app

You can try out razzle easily with the help of [create-razzle-app](https://www.npmjs.com/package/create-razzle-app)


```bash
npx create-razzle-app my-proj
cd my-proj
npm start
```

## How Razzle works (the secret sauce)

**TL;DR**: 2 configs, 2 ports, 2 webpack instances, both watching and hot reloading the same filesystem, in parallel during development and a little `webpack.output.publicPath` magic.

In development mode (`razzle start`), Razzle bundles both your client and server code using two different webpack instances running with Hot Module Replacement in parallel. While your server is bundled and run on whatever port you specify in `src/index.js` (`3000` is the default), the client bundle (i.e. entry point at `src/client.js`) is served via `webpack-dev-server` on a different port (`3001` by default) with its `publicPath` explicitly set to `localhost:3001` (and not `/` like many other setups do). Then the server's html template just points to the absolute url of the client JS: `localhost:3001/static/js/client.js`. Since both webpack instances watch the same files, whenever you make edits, they hot reload at _exactly_ the same time. Best of all, because they use the same code, the same webpack loaders, and the same babel transformations, you never run into a React checksum mismatch error.

## Inspiration

- [jaredpalmer/backpack](https://github.com/jaredpalmer/backpack)
- [nytimes/kyt](https://github.com/nytimes/kyt)
- [facebookincubator/create-react-app](https://github.com/facebookincubator/create-react-app)
- [humblespark/sambell](https://github.com/humblespark/sambell)
- [zeit/next.js](https://github.com/zeit/next.js)

#### Author

- [Jared Palmer](https://twitter.com/jaredpalmer)

---

MIT License

## Contributors

Thanks goes to these wonderful people ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://jaredpalmer.com"><img src="https://avatars2.githubusercontent.com/u/4060187?v=4" width="100px;" alt=""/><br /><sub><b>Jared Palmer</b></sub></a><br /><a href="#question-jaredpalmer" title="Answering Questions">💬</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=jaredpalmer" title="Code">💻</a> <a href="#design-jaredpalmer" title="Design">🎨</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=jaredpalmer" title="Documentation">📖</a> <a href="#example-jaredpalmer" title="Examples">💡</a> <a href="#ideas-jaredpalmer" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/jaredpalmer/razzle/pulls?q=is%3Apr+reviewed-by%3Ajaredpalmer" title="Reviewed Pull Requests">👀</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=jaredpalmer" title="Tests">⚠️</a> <a href="#tool-jaredpalmer" title="Tools">🔧</a></td>
    <td align="center"><a href="https://jari.io"><img src="https://avatars3.githubusercontent.com/u/1415847?v=4" width="100px;" alt=""/><br /><sub><b>Jari Zwarts</b></sub></a><br /><a href="#question-jariz" title="Answering Questions">💬</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=jariz" title="Code">💻</a> <a href="#ideas-jariz" title="Ideas, Planning, & Feedback">🤔</a> <a href="#plugin-jariz" title="Plugin/utility libraries">🔌</a> <a href="https://github.com/jaredpalmer/razzle/pulls?q=is%3Apr+reviewed-by%3Ajariz" title="Reviewed Pull Requests">👀</a></td>
    <td align="center"><a href="http://twitter.com/dan_abramov"><img src="https://avatars0.githubusercontent.com/u/810438?v=4" width="100px;" alt=""/><br /><sub><b>Dan Abramov</b></sub></a><br /><a href="https://github.com/jaredpalmer/razzle/commits?author=gaearon" title="Code">💻</a> <a href="#ideas-gaearon" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="http://ericclemmons.github.com/"><img src="https://avatars0.githubusercontent.com/u/15182?v=4" width="100px;" alt=""/><br /><sub><b>Eric Clemmons</b></sub></a><br /><a href="https://github.com/jaredpalmer/razzle/commits?author=ericclemmons" title="Code">💻</a> <a href="#ideas-ericclemmons" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://www.linkedin.com/in/zinohofmann/"><img src="https://avatars3.githubusercontent.com/u/17142193?v=4" width="100px;" alt=""/><br /><sub><b>Zino Hofmann</b></sub></a><br /><a href="#example-HofmannZ" title="Examples">💡</a></td>
    <td align="center"><a href="https://www.linkedin.com/in/lucasterra7/"><img src="https://avatars2.githubusercontent.com/u/441058?v=4" width="100px;" alt=""/><br /><sub><b>Lucas Terra</b></sub></a><br /><a href="https://github.com/jaredpalmer/razzle/commits?author=lucasterra" title="Code">💻</a> <a href="#example-lucasterra" title="Examples">💡</a> <a href="#plugin-lucasterra" title="Plugin/utility libraries">🔌</a></td>
    <td align="center"><a href="https://www.linkedin.com/in/ray-andrew/"><img src="https://avatars1.githubusercontent.com/u/4437323?v=4" width="100px;" alt=""/><br /><sub><b>Ray Andrew</b></sub></a><br /><a href="https://github.com/jaredpalmer/razzle/commits?author=rayandrews" title="Code">💻</a> <a href="#example-rayandrews" title="Examples">💡</a> <a href="#plugin-rayandrews" title="Plugin/utility libraries">🔌</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/Nimaa77"><img src="https://avatars2.githubusercontent.com/u/25016067?v=4" width="100px;" alt=""/><br /><sub><b>nimaa77</b></sub></a><br /><a href="#question-Nimaa77" title="Answering Questions">💬</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=Nimaa77" title="Code">💻</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=Nimaa77" title="Documentation">📖</a> <a href="#example-Nimaa77" title="Examples">💡</a> <a href="#ideas-Nimaa77" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/jaredpalmer/razzle/pulls?q=is%3Apr+reviewed-by%3ANimaa77" title="Reviewed Pull Requests">👀</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=Nimaa77" title="Tests">⚠️</a> <a href="#tool-Nimaa77" title="Tools">🔧</a></td>
    <td align="center"><a href="https://github.com/fivethreeo"><img src="https://avatars2.githubusercontent.com/u/410?v=4" width="100px;" alt=""/><br /><sub><b>Øyvind Saltvik</b></sub></a><br /><a href="#question-fivethreeo" title="Answering Questions">💬</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=fivethreeo" title="Code">💻</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=fivethreeo" title="Documentation">📖</a> <a href="#example-fivethreeo" title="Examples">💡</a> <a href="#ideas-fivethreeo" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/jaredpalmer/razzle/pulls?q=is%3Apr+reviewed-by%3Afivethreeo" title="Reviewed Pull Requests">👀</a> <a href="https://github.com/jaredpalmer/razzle/commits?author=fivethreeo" title="Tests">⚠️</a> <a href="#tool-fivethreeo" title="Tools">🔧</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors) specification. Contributions of any kind welcome!
