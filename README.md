# Deno Snowpack Demo

## What is this?

This demo shows how it's possible to use NPM packages (ones with an ES module build) with the [Deno](https://deno.land/) JavaScript runtime, thanks to [Snowpack](https://www.snowpack.dev/). You can find ESM packages to try with Deno on [Pika](https://www.pika.dev/).

In the demo, a [Preact](https://preactjs.com/) element tree is rendered to a string and logged to the console. [HTM](https://github.com/developit/htm) is used rather than JSX to avoid the need for a transpilation step.

## How do I try it?

1. Install dependencies with NPM:

   ```sh
   npm install
   ```

   Snowpack should automatically run after installation - if not, run:

   ```sh
   npx snowpack
   ```

2. Run the demo with Deno:

   ```sh
   deno index.js
   ```

   Or, using Node.js - the output should be the same:

   ```sh
   node index.js
   ```

## How does this work?

Snowpack re-packs NPM dependencies with an ESM build into single JS files. Deno scripts can then import these files, provided they don't use `require` or rely on any runtime-specific APIs.

## Does Snowpack itself run on Deno?

No. Although Snowpack enables using other NPM packages in Deno, Snowpack itself cannot run on Deno without further work, since it relies on both the Node.js module system and Node-specific APIs.

## Does this work with [my favourite package]?

Probably not - this only works with packages that can both be built as pure ES modules, and that don't require the use of any Node-specific or web-specific JavaScript APIs. Supporting the larger Node.js ecosystem would be a more ambitious project, as Deno doesn't support CommonJS imports (i.e. `require`), and a compatibility layer would need to be created to support Node-specific APIs.

Things which likely **will** work:

- Packages that can run in both the browser and the server, and don't require network/filesystem interaction, e.g. Preact
- Packages that don't rely on Node-specific APIs (e.g. filesystems)
- Utility libraries, e.g. Lodash

Things that **won't** work:

- Packages that rely on Node-specific or web-specific APIs
- Packages that rely on native extensions
- Packages that rely on the the Node.js module system (`require`, `module` etc)
