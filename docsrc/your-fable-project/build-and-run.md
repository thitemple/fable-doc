---
title: Build & Run
---

# Build & Run

Your project is ready? Then it's time to build and run it.

This process, however, is different depending on whether we are still in development or we are already preparing the project to deploy it to production. In development we don't care so much about optimizations and we want fast builds so we can see the results of our changes on-screen almost immediately. While for production we can endure a slower build in order to get JS code that is more optimized.

> In this document we assume you are using [fable-loader](https://www.npmjs.com/package/fable-loader) with [Webpack](https://webpack.js.org/) to build your Fable web app. If you use other tools, [like fable-splitter](https://www.npmjs.com/package/fable-splitter), please refer to their documentation.

Webpack can be a bit difficult to configure. Most of the [samples](https://github.com/fable-compiler/fable2-samples) have a `webpack.config.js` file that you can use for reference. And there's also a [webpack config template for Fable](https://github.com/fable-compiler/webpack-config-template/blob/master/webpack.config.js) that is prepared to work in most projects.

Whenever Webpack encounters an F# file, it will call the fable-loader which in turn spawns a [fable-compiler](https://www.npmjs.com/package/fable-compiler) process to translate the F# files to JS. The generated code will be sent back to Webpack that will merge it into the final bundle.

> Whenever you want to use a new version of Fable in your project, you only to update the fable-compiler package: `npm update fable-compiler`.

## Development

Even if we already have our own server, when developing our frontend we want a server that is capable of detecting changes in the code and load them without restarting the app! This what [webpack-dev-server](https://github.com/webpack/webpack-dev-server) does, so normally we'll be running it during development: `npx webpack-dev-server --mode development`.

> In most Fable projects, we just [assume webpack-dev-server runs in development](https://github.com/fable-compiler/webpack-config-template/blob/34c04e8474e1a6e94698dd1e14e5a197733a65f2/webpack.config.js#L42-L44) so you won't see the `--mode` argument explicitly set very often.

If you use [npm-scripts](https://docs.npmjs.com/misc/scripts) as shortcuts for common actions, it's customary to use `npm start` to run in development mode. In npm scripts, you can call executables from `node_modules/.bin` directly, so in order to call webpack-dev-server with the start command you only need to add the following to your `package.json`:

```json
  "scripts": {
    "start": "webpack-dev-server"
  },
```

> If you also have your own server, you probably want to redirect API calls to it. You can use the [devServer.proxy](https://webpack.js.org/configuration/dev-server#devserverproxy) Webpack configuration option for that.

The webpack-dev-server will keep running until you kill the process, picking up the changes in your code after you save a file. If you use [Hot Module Replacement](https://elmish.github.io/hmr/) it will try to inject the changes without restarting the app. Otherwise it will just refresh the web page.

Note that webpack-dev-server serves the generated files from memory and doesn't actually write to disk. We will do that in the next step: building for production!

## Production

When preparing the files for deployment, we don't need a special server. We can call Webpack CLI directly in production mode to enable optimizations like [JS minification](https://webpack.js.org/configuration/optimization#optimizationminimize): `npx webpack --mode production`.

> As before, in most configurations you don't need to set the `--mode` argument explicitly. And it's also customary to have a "build" (or sometimes "deploy") npm-script for this operation:

```json
  "scripts": {
    "start": "webpack-dev-server",
    "build": "webpack"
  },
```

Webpack will run only once and will write the generated files in the [output.path](https://webpack.js.org/configuration/output#outputpath). This is the directory you fave to deploy to your host!

## I don't want to use Webpack

Then, depending on the sample you've chosen, build options may differ. Please refer to the README file for the chosen sample to get more information.