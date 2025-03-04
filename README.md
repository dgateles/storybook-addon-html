# Storybook Addon HTML

*THIS ADDON IS A COPY FROM https://github.com/whitespace-se/storybook-addon-html WITH FIXES THAT NOT PROVIDED BY AUTHOR.*

This addon for Storybook adds a tab that displays the compiled HTML for each
story. It uses [highlight.js](https://highlightjs.org/) for syntax highlighting.

![Animated preview](https://raw.githubusercontent.com/dgateles/storybook-addon-html/master/image.gif)

## Getting Started

Install the addon and its dependencies.

With NPM:

```sh
npm i --save-dev @dgateles/storybook-addon-html prettier react-syntax-highlighter
```

With Yarn:

```sh
yarn add -D @dgateles/storybook-addon-html prettier react-syntax-highlighter
```

### Register addon

```js
// .storybook/main.js

module.exports = {
  // ...
  addons: [
    "@dgateles/storybook-addon-html",
    // ...
  ],
};
```

## Usage

The HTML is formatted with Prettier. You can override the Prettier config
(except `parser` and `plugins`) by providing an object following the
[Prettier API override format](https://prettier.io/docs/en/options.html) in the
`html` parameter:

```js
// .storybook/preview.js

export const parameters = {
  // ...
  html: {
    prettier: {
      tabWidth: 4,
      useTabs: false,
      htmldgatelesSensitivity: "strict",
    },
  },
};
```

You can override the wrapper element selector used to grab the component HTML.

```js
export const parameters = {
  html: {
    root: "#my-custom-wrapper", // default: #root
  },
};
```

Some frameworks put comments inside the HTML. If you want to remove these you
can use the `removeComments` parameter. Set it to `true` to remove all comments
or set it to a regular expression that matches the content of the comments you
want to remove.

```js
export const parameters = {
  html: {
    removeComments: /^\s*remove me\s*$/, // default: false
  },
};
```

You can also use the `removeEmptyComments` parameter to remove only empty
comments like `<!---->` and `<!-- -->`.

```js
export const parameters = {
  html: {
    removeEmptyComments: true, // default: false
  },
};
```

You can override the `showLineNumbers` and `wrapLines` settings for the syntax
highlighter by using the `highlighter` parameter:

```js
export const parameters = {
  html: {
    highlighter: {
      showLineNumbers: true, // default: false
      wrapLines: false, // default: true
    },
  },
};
```

Another way of hiding unwanted code is to define the `transform` option. It
allows you to perform any change to the output code, e.g. removing attributes
injected by frameworks.

```js
html: {
  transform: (code) => {
    // Remove attributes `_nghost` and `ng-reflect` injected by Angular:
    return code.replace(/(?:_nghost|ng-reflect).*?="[\S\s]*?"/g, "");
  };
}
```
