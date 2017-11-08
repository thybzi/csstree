<img align="right" width="111" height="111"
     alt="CSSTree logo"
     src="https://cloud.githubusercontent.com/assets/270491/19243723/6f9136c6-8f21-11e6-82ac-eeeee4c6c452.png"/>

# CSSTree

[![NPM version](https://img.shields.io/npm/v/css-tree.svg)](https://www.npmjs.com/package/css-tree)
[![Build Status](https://travis-ci.org/csstree/csstree.svg?branch=master)](https://travis-ci.org/csstree/csstree)
[![Coverage Status](https://coveralls.io/repos/github/csstree/csstree/badge.svg?branch=master)](https://coveralls.io/github/csstree/csstree?branch=master)
[![Join the CSSTree chat at https://gitter.im/csstree/csstree](https://badges.gitter.im/csstree/csstree.svg)](https://gitter.im/csstree/csstree)
[![Twitter](https://img.shields.io/badge/Twitter-@csstree-blue.svg)](https://twitter.com/csstree)

CSSTree – set of tools to work with CSS, including [fast](https://github.com/postcss/benchmark) detailed parser (string->AST), walker (AST traversal), generator (AST->string) and even lexer (validation and matching) based on knowledge of spec and browser implementations (see [API schema](#top-level-api) for details). The main goal is to be efficient and W3C spec compliant, with focus on analyzing and source-to-source processing.

> Work in progress. The project in alpha stage since some parts need further experiments, AST format and API are subjects to change. However it's stable enough and used by packages like [CSSO](https://github.com/css/csso) (CSS minifier) in production.

## Features

- **Detailed parsing with customisation**

  By default CSSTree parses CSS as detailed as possible, i.e. each single logical part is representing with its own AST node (see [AST format](docs/ast.md) for all possible node types). The parsing detail level can be changed through [parser options](docs/parsing.md#parsesource-options), for example, you can disable parsing of selectors or declarations for component parts.

- **Tolerant by design**

  Parser behaves as [spec says](https://www.w3.org/TR/css-syntax-3/#error-handling): "When errors occur in CSS, the parser attempts to recover gracefully, throwing away only the minimum amount of content before returning to parsing as normal". The parser departs from the specification and does not throw away bad content, but wraps it in special nodes, which allows processing it later.

- **Fast and efficient**

  CSSTree is designed with focus on performance and effective memory consumption. Therefore it's [one of the fastest CSS parsers](https://github.com/postcss/benchmark) at the moment.

- **Syntax validation**

  The build-in lexer can validate CSS against syntaxes defined by W3C. CSSTree uses [mdn/data](https://github.com/mdn/data/) as basis for lexer's dictionaries and extends them with vendor specific and legacy syntaxes. Lexer can only check the values of declarations currently, but this feature will be extended to other parts of the CSS in the future.

## Docs

- [Parsing CSS into AST](docs/parsing.md)
- [AST format](docs/ast.md)
- [Translate AST to string](docs/translate.md)
- [AST traversal](docs/traversal.md)
- [Utils to work with AST](docs/utils.md)

## Tools

* [AST Explorer](https://astexplorer.net/#/gist/244e2fb4da940df52bf0f4b94277db44/e79aff44611020b22cfd9708f3a99ce09b7d67a8) – explore CSSTree AST format with zero setup
* [CSS syntax reference](https://csstree.github.io/docs/syntax.html)
* [CSS syntax validator](https://csstree.github.io/docs/validator.html)

## Related projects

* [csstree-validator](https://github.com/csstree/validator) – NPM package to validate CSS
* [stylelint-csstree-validator](https://github.com/csstree/stylelint-validator) – plugin for stylelint to validate CSS
* [Grunt plugin](https://github.com/sergejmueller/grunt-csstree-validator)
* [Gulp plugin](https://github.com/csstree/gulp-csstree)
* [Sublime plugin](https://github.com/csstree/SublimeLinter-contrib-csstree)
* [VS Code plugin](https://github.com/csstree/vscode-plugin)
* [Atom plugin](https://github.com/csstree/atom-plugin)

## Usage

Install with npm:


```
> npm install css-tree
```

Use in your code:

```js
var csstree = require('css-tree');
var ast = csstree.parse('.example { world: "!" }');

csstree.walk(ast, function(node) {
    if (node.type === 'ClassSelector' && node.name === 'example') {
        node.name = 'hello';
    }
});

console.log(csstree.translate(ast));
// .hello{world:"!"}
```

## Top level API

![API map](https://cdn.rawgit.com/csstree/csstree/master/docs/api-map.svg)

## License

MIT

Syntax matching uses [mdn/data](https://github.com/mdn/data) by Mozilla Contributors
