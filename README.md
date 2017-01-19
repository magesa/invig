[![Build Status](https://travis-ci.org/kvz/invig.svg?branch=master)](https://travis-ci.org/kvz/invig)

> Here's another one of my more upsetting projects. 

# Invig

Breathe new life into legacy code bases by automatically:

 - Transpiling CoffeeScript to ES6
 - Transpiling ES5 to ES6 (without the stuff that recent Node hasn't nailed yet (e.g. we stick to `require` vs `import` for now))
 - Applying Standard linting via eslint
 - Adding the necessary linting and building boilerplate to the project's package.json
 
Invig does this in a highly opinionated, non-configurable, and **destructive** way. 

**WARNING**

Make sure your sources are safe under version control before point invig to your codebase. 
After that, have fun breathing new life into your legacy project 🤗💨🌿 

## Why

I got tired of context switching between ES5, ES6, CoffeeScript, and different code conventions.

The tools are there now. It's just a matter of stringing them together, and all code can be present day ECMA and look uniformly styled.

## Install

```bash
yarn global add invig || npm install --global invig
```

## Use

Port one CoffeeScript file to ES6 (deleting the old `.coffee` file.):

```bash
invig --src old-file.coffee
```

Port one ES5 file to ES6 (original file destroyed forever unless under version control):

```bash
invig --src old-file.js
```

Port an entire directory of CoffeeScript or ES5 files to ES6 (In place. The original `src/` contents are destroyed forever unless under version control):

```bash
invig --src src/
```

Ignore any error and continue with the operation for the next file. By default, Invig will abort on the first error for manual intervention:

```bash
invig --src src/ --nobail
```

The recommended way to use Invig is to:

1. have a clean Git working tree first
1. `git checkout -b es6`
2. run invig on it
3. apply manual fixes where the automation still falls short (Invig will tell you)
4. once you like the git diff, commit, push, send a PR for your `es6` branch (btw, the [GitHub Desktop](https://desktop.github.com) app makes for a great inspection tool here. "But I wield my git cli like a god and UIs are for noobz!". Sure, have it your way)

## State

Invig is Young! Pre-`1.0.0`, we're allowing ourselves to make breaking changes at any release.

## Gotchas

- Although Invig is destructive in nature, it currently leaves your `build` runtasks alone if you have already defined them. If you currently have
CoffeeScript build tasks, remove them first, so that Invig can write the new one. 
Same goes for the `lint`, `fix`, and `build:watch` scripts, as well as the `.eslintrc`, and `.babelrc` files. The advantage of this that you 
can run Invig multiple times even though you have customized these components that are used in the modern setup.
- Support for <https://github.com/jlongster/prettier> is already added, but disabled, as there are still some issues (like adding trailing commas to function arguments). It's traveling fast tho, so check back soon to see if we can enable it as a pre-step to eslint standard, that will give us `go fmt`-like strictness. If you want to enable Prettier, prefix your Invig commands with `env INVIG_PRETTIER=1 `

## Limitations

- Invig needs a sense of a project so it can add eslint config and similar, so there needs to be a `package.json`, and this gets
**modified in place**, also.

## Troubleshooting

Sometimes failures happen because eslint wasn't able to make all the beautifications automatically. 
You can then open (CMD+Click if you set up your terminal correctly) the file in your editor, make the changes by hand,
and 

## Thanks to

Invig is just a wrapper around these beasts:

- <https://github.com/decaffeinate/decaffeinate>
- <http://lebab.io>
- <http://eslint.org>
- <https://github.com/jlongster/prettier>
- <http://standardjs.com>

## Todo

- [ ] Rewrite coffeescript mocha to `mocha --require babel-polyfill --compilers js:babel-register`

## Authors

- [Kevin van Zonneveld](https://transloadit.com/about/#kevin)

## License

Copyright (c) 2017 Kevin van Zonneveld. Licenses under [MIT](LICENSE).
