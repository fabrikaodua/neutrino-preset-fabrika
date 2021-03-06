# Fabrika Neutrino preset

`neutrino-preset-fabrika` is a [Neutrino](https://neutrino.js.org) preset for creation of web applications for web platforms.

## Features

- Zero upfront configuration necessary to start developing and building a Svelte web app
- Modern Babel compilation supporting ES modules, last several major browser versions, async functions, dynamic imports, ES class properties, rest spread operators and automatic polyfills bound to platforms
- Webpack loaders for importing HTML Svelte components, CSS, images, icons, and fonts
- Webpack Dev Server during development on "localhost" and local network IP for external devices access
- Automatic creation of HTML pages, no templating of `index.html` necessary
- Hot reloading support
- Tree-shaking to create smaller bundles
- Production-optimized bundles with Babili minification, source maps and easy chunking
- Testing with Jest
- Source watching for re-running of tests on change
- Collecting test coverage information and generating report
- ESlint code analyze
- Stylelint code analyze

## Requirements

- Node.js v6.9+
- Neutrino v6

## Installation

`neutrino-preset-fabrika` can be installed from NPM. Make sure `neutrino` and `neutrino-preset-fabrika` are development dependencies in your project.

**package.json**
```json
"devDependencies": {
  "neutrino": "latest",
  "neutrino-preset-fabrika": "latest"
},
```

And add the new file `.neutrinorc.js` in the root of the project:

**.neutrinorc.js**
```js
module.exports = {
  use: [
    'neutrino-preset-fabrika'
  ]
}
```

Install all you project dependencies by calling

```bash
npm install
```

## Project Layout

`neutrino-preset-fabrika` follows the standard [project layout](https://neutrino.js.org/project-layout) specified by Neutrino. This means that by default all project source code should live in a directory named `src` in the root of the project. This includes JavaScript files, CSS stylesheets, images, and any other assets that would be available to your compiled project. Only files explicitly imported or lazy loaded to your project will be bundled.

Project test code should live in a directory named `test` in the root of the project. Test files end in either `_test.js` or `.test.js`.

## Quick start

### Source code

After installing Neutrino and the Fabrika preset, add a new directory named `src` in the root of the project, with a single JS file named `index.js` in it. You can mount you application to the document `<body>`. Edit your `src/index.js` file with the following:

```js

import './main.css'

document.body.innerHTML = 'Application started'
```

You can change this code base to better match your needs.

### Tests
You can create also `test/index.test.js` as an entry point for your test. To run tests against files from your source code, simply import them. [Jest](https://facebook.github.io/jest/) framework is used in this preset so your tests will look like this:

 ```js
import module from '../src/module.js'

describe('module', () => {
  it('is truthy', () => {
    expect(module).toBeTruthy();
  });
});
```

### Tasks

Now edit your project's `package.json` to add commands for starting and building the application:

```json
{
  "scripts": {
    "start": "neutrino start",
    "build": "neutrino build",
    "test": "neutrino test",
    "test:watch": "neutrino test --watch",
    "coverage": "neutrino test --coverage"
  }
}
```

Start the app. 

```bash
❯ npm start
✔ Development server running on: http://localhost:3000
✔ Build completed
```

The application will automatically open in a default browser with a local network IP. The same address may be used on any device that is connected to the same local network. For example it may be useful for mobile versions development.

This preset is compatible with different frameworks. It allows to flexibly setup entry point for different types of projects.

### Start with VueJS application

VueJS framework uses `.vue` files as components. For quick start you can use this sample. You can mount your application to the document `<body>`. Edit your `src/index.js` file with the following:

**index.js**
```js
import Vue from 'vue';
import Body from './body.vue';

new Vue({ // eslint-disable-line no-new
  el: 'body',
    render(callback) {
    return callback(Body);
  }
});
```

**body.vue**
```html
<script>
  export default {};
</script>

<style src="./common.css" />

<template>
  <body>
    Application started
  </body>
</template>

```

You can change this code base to better match your needs.


### Start with Svelte application

Svelte framework uses `.html` files as components. For quick start you can use this sample. You can mount you application to the document `<body>`. Edit your `src/index.js` file with the following:

**index.js**
```js
import Body from './body.html'
import './main.css'

new Body({ // eslint-disable-line no-new
  target: document.body
})
```

**body.html**
```html
<div>Application started</div>

<style></style>

<script>
  export default {};
</script>
```

You can change this code base to better match your needs.

## Building

`neutrino-preset-fabrika` builds static assets to the `build` directory by default when build command is run.

```bash
❯ npm run build
```

You can either serve or deploy the contents of this build directory as a static site.

### Static assets

If you wish to copy files to the build directory that are not imported from application code, you can place them in a directory within `src` called `static`. All files in this directory will be copied from `src/static` to `build/static`.

## Testing

```bash
❯ npm test

 PASS  test/index.test.js
  module
    ✓ is truthy (2ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.972s
Ran all test suites.
```

### Executing single tests

By default this preset will execute every test file located in your test directory ending in the appropriate file
extension.

### Watching for changes

`neutrino-preset-jest` can watch for changes on your source directory and subsequently re-run tests. Simply run command:

```bash
❯ npm test:watch
```

### Coverage reporting

Jest has an integrated coverage reporter, which requires no configuration. To collect test coverage information and
generate a report:

```bash
❯ npm run coverage
```

## Hot Reloading

`neutrino-preset-fabrika` supports Hot Reloading of files that was changed. Hot Module Replacement is supported only in CSS files and Vue components. Other types of modules will completely reload the page on change.

Using dynamic imports with `import()` will automatically create split points and hot replace those modules upon modification during development.

## Linting

`neutrino-preset-fabrika` has a built-in support of ESlint and Stylelint. But for highlighting of errors in code editors config files should be created in the project root. The static analyzes will be performed automatically on build and start.

### ESLint

To enable ESlint in the code editor install a corresponding editor extension and create `.eslintrc.js` file in the project root

**.eslintrc.js**
```js
const { Neutrino } = require('neutrino')
const api = Neutrino()
module.exports = api.call('eslintrc')
```

### Stylelint

To enable Stylelint in the code editor install a corresponding editor extension and create `.stylelintrc.js` file in the project root

**.stylelintrc.js**
```js
const { Neutrino } = require('neutrino')
const api = Neutrino()
module.exports = api.call('stylelintrc')
```

## Preset options

You can provide custom options and have them merged with this preset's default options to easily affect how this preset builds. You can modify the preset settings from `.neutrinorc.js` by overriding with an options object. Use
an array pair instead of a string to supply these options in `.neutrinorc.js`.

The following shows how you can pass an options object to the preset and override its options, showing the defaults:

**.neutrinorc.js**
```js
module.exports = {
  use: [
    ['neutrino-preset-fabrika', {
      // options related to generating the HTML document
      html: {
        title: `${name} ${version}`,
        mobile: true
      },

      // options related to a development server
      server: {
        https: false,
        public: true,
        port: 3000,
        open: true
      },

      // supported browsers in a Browser List format
      browsers: [
        'last 3 versions'
      ]
    }]
  ]
};
```

*Example: Enable HTTPS, disable auto-opening of a browser, change the page title, define supported browsers:*

**.neutrinorc.js**
```js
module.exports = {
  use: [
    ['neutrino-preset-svelte', {
      // Example: disable auto open in browser and enable SSL
      server: {
        https: true,
        open: false
      },

      // Example: change the page title
      html: {
        title: 'Web App'
      },

      // Example: change supported browsers
      browsers: [
        'last 1 version',
        'ie >= 10'
      ]
    }]
  ]
};
```


