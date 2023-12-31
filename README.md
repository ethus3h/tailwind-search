# @dtinth’s Tailwind CSS Class Search updated by @ethus3h for Tailwind 3

Having trouble memorizing all the utility classes in Tailwind? Remembered the CSS code, but did not remember which is the corresponding Tailwind CSS utility class? [Search for it here! https://tailwind-class-search.pages.dev/](https://tailwind-class-search.pages.dev/)

This little web application parses the Tailwind CSS file right from `unpkg.com` using [css-tree](https://www.npmjs.com/package/css-tree), and generates a searchable index that lets you search for a utility class’s name, if you know the generated CSS code you want. The web app is built with [Vue.js](https://vuejs.org/), fast fuzzy-searching is provided by [fuzzysort](https://www.npmjs.com/package/fuzzysort) and the result list is lazily rendered with help of [vue-virtual-scroller](https://www.npmjs.com/package/vue-virtual-scroller).

- When do I use `font-`? e.g. `font-bold`
- When do I use `text-`? e.g. `text-lg` even though it’s `font-size`
- When do I use _neither?_ e.g. `italic`
- Most of the time I know what kind of CSS code I want, but couldn't correctly recall the class name.
- This app also lets you check whether a class is available in Tailwind’s default build. (When I prototype apps, I like to use the Tailwind CSS default builds straight from the CDN.)

## Development

- **to build Tailwind** - run `npx yarn css:build`

- **No build system needed.** Just clone the Git repository, open `index.html` file in your browser. Edit, save and refresh. Append `?dev=1` to URL to load full Tailwind CSS file.

## Usage in Node

```js
const fs = require('fs')
const tailwindCssClassSearch = require('@dtinth/tailwind-css-class-search')

// Read CSS file
const css = fs.readFileSync(require.resolve('tailwindcss/dist/tailwind.css'))

// Generate a search index
const searchIndex = await tailwindCssClassSearch(css)

// Inspect all entries
searchIndex.entries // => Array(12526)

// Search
searchIndex.search('font-size') // Array(50)
```

## Preparing for deployment

Since the full generated tailwind is 1mb large, we use [purgecss](https://purgecss.com/CLI) to remove unused selectors and reduce the CSS file size to 20kb.

```
yarn build
```

## VS Code integration

See the [`contrib/vscode` folder](./contrib/vscode) for more info on experimental VS Code integration.
