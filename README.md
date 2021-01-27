# Just messing around

Just a repo messing with svelte and sapper!

## Getting started

Once you have cloned the project, install dependencies and run the project in development mode:

```bash
npm install #
npm run dev --site={site} # where site is one of the directory names inside src/sites
```

This will start the development server on [localhost:3000](http://localhost:3000). Open it and click around.

`@sapper` dependencies are resolved through `src/node_modules/@sapper`, which is created during the build. You therefore need to run or build the project once to avoid warnings about missing dependencies.

## Directory structure

Sapper expects to find two directories in the root of your project —  `src` and `static`.


### src

The [src](src) directory contains all of the contents for the sites

## src/global
contains globally shared assets

## src/global/components
global components

## src/global/styles
global styles (should include scss variables,  mixins, etc..)

### src/sites
Holds src for sites

#### src/sites/{site}/routes

This is the heart of your Sapper app. There are two kinds of routes — *pages*, and *server routes*.

**Pages** are Svelte components written in `.svelte` files. When a user first visits the application, they will be served a server-rendered version of the route in question, plus some JavaScript that 'hydrates' the page and initialises a client-side router. From that point forward, navigating to other pages is handled entirely on the client for a fast, app-like feel. (Sapper will preload and cache the code for these subsequent pages, so that navigation is instantaneous.)

**Server routes** are modules written in `.js` files, that export functions corresponding to HTTP methods. Each function receives Express `request` and `response` objects as arguments, plus a `next` function. This is useful for creating a JSON API, for example.

There are three simple rules for naming the files that define your routes:

* A file called `src/routes/about.svelte` corresponds to the `/about` route. A file called `src/routes/blog/[slug].svelte` corresponds to the `/blog/:slug` route, in which case `params.slug` is available to the route
* The file `src/routes/index.svelte` (or `src/routes/index.js`) corresponds to the root of your app. `src/routes/about/index.svelte` is treated the same as `src/routes/about.svelte`.
* Files and directories with a leading underscore do *not* create routes. This allows you to colocate helper modules and components with the routes that depend on them — for example you could have a file called `src/routes/_helpers/datetime.js` and it would *not* create a `/_helpers/datetime` route.


#### src/sites/{site}/node_modules/images

Images added to `src/sites/{site}/node_modules/images` can be imported into your code using `import 'images/<filename>'`. They will be given a dynamically generated filename containing a hash, allowing for efficient caching and serving the images on a CDN.

See [`index.svelte`](src/routes/index.svelte) for an example.


#### src/sites/{sites}/node_modules/@sapper

This directory is managed by Sapper and generated when building. It contains all the code you import from `@sapper` modules.


### src/sites/{site}/static

The [static](static) directory contains static assets that should be served publicly. Files in this directory will be available directly under the root URL, e.g. an `image.jpg` will be available as `/image.jpg`.

The default [service-worker.js](src/service-worker.js) will preload and cache these files, by retrieving a list of `files` from the generated manifest:

```js
import { files } from '@sapper/service-worker';
```

If you have static files you do not want to cache, you should exclude them from this list after importing it (and before passing it to `cache.addAll`).

Static files are served using [sirv](https://github.com/lukeed/sirv).


## Bundler configuration

Sapper uses Rollup or webpack to provide code-splitting and dynamic imports, as well as compiling your Svelte components. With webpack, it also provides hot module reloading. As long as you don't do anything daft, you can edit the configuration files to add whatever plugins you'd like.


### Aliases

- '@' points to `src/global` and can be used in any file