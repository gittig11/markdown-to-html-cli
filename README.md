markdown-to-html-cli
===
<!--rehype:style=display: flex; height: 230px; align-items: center; justify-content: center; font-size: 38px;-->

[![Downloads](https://img.shields.io/npm/dm/markdown-to-html-cli.svg?style=flat)](https://www.npmjs.com/package/markdown-to-html-cli)
[![npm version](https://img.shields.io/npm/v/markdown-to-html-cli.svg)](https://www.npmjs.com/package/markdown-to-html-cli)
[![Build and Test](https://github.com/jaywcjlove/markdown-to-html-cli/actions/workflows/ci.yml/badge.svg)](https://github.com/jaywcjlove/markdown-to-html-cli/actions/workflows/ci.yml)
[![Coverage Status](https://jaywcjlove.github.io/markdown-to-html-cli/badges.svg)](https://jaywcjlove.github.io/markdown-to-html-cli/lcov-report/)
[![中文文档](https://jaywcjlove.github.io/sb/lang/chinese.svg)](README-zh.md)

Converts markdown text to HTML, Provide command line tools and methods. If you are simply converting a small number of Markdown files (or text) into HTML pages, this is very helpful for you.

## Usage

Used in Github [Actions](https://github.com/actions).

```yml
- run: npm i markdown-to-html-cli -g
- run: markdown-to-html --output coverage/index.html
```

Using With Command.

```js
{
  "scripts": {
    "start": "markdown-to-html --output coverage/index.html"
  },
  "devDependencies": {
    "markdown-to-html-cli": "latest"
  }
}
```

Used in [Nodejs](https://nodejs.org).

```js
import { create } from 'markdown-to-html-cli';

const html = create({
  markdown: 'Hello World! **Bold**\n# Title',
  document: {
    style: ['body { background: red; }'],
  }
});
// => HTML String
```

## Install

```shell
$ npm i markdown-to-html-cli
```

## Configure in package.json

The configuration can be specified through `--config="config/conf.json"`, It can be in `package.json` by default.

```js
{
  "markdown-to-html": {
    "document": {
      "title": "markdown-to-html-cli",
      "description": "Command line tool generates markdown as html.",
      "style": "body { color: red; }",
      "meta": [
        { "description": "Command line tool generates markdown as html." },
        { "keywords": "store,localStorage,lightweight,JavaScript" }
      ]
    },
    "favicon": "data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🌐</text></svg>",
    "github-corners": "https://github.com/jaywcjlove/markdown-to-html-cli",
    "reurls": {
      "README-zh.md": "index.zh.html",
      "README.md": "index.html"
    }
  }
}
```

- [`name`](https://github.com/jaywcjlove/markdown-to-html-cli/blob/308ca37aa5b9ae846a7835092a183d0ed73a8dc4/package.json#L2) -> `'markdown-to-html'.title` - Define the content of the `<title>` document title!
- [`description`](https://github.com/jaywcjlove/markdown-to-html-cli/blob/308ca37aa5b9ae846a7835092a183d0ed73a8dc4/package.json#L4) -> `'markdown-to-html'.description` - Define a description of your web page.
- [`repository.url`](https://github.com/jaywcjlove/markdown-to-html-cli/blob/308ca37aa5b9ae846a7835092a183d0ed73a8dc4/package.json#L22) -> `'markdown-to-html'.github-corners` - Add a Github corner to your project page.
- [`keywords`](https://github.com/jaywcjlove/markdown-to-html-cli/blob/308ca37aa5b9ae846a7835092a183d0ed73a8dc4/package.json#L24-L30) -> `'markdown-to-html'.document.meta` - Define keywords for search engines.

## Command Help

```bash
Usage: markdown-to-html [options] [--help|h]

Options:

  --author          Define the author of a page.
  --config, -o      Specify the configuration file. Default: "<process.cwd()>/package.json".
  --description     Define a description of your web page.
  --favicon         Add a Favicon to your Site.
  --github-corners  Add a Github corner to your project page.
  --github-corners-fork  Github corners style.
  --keywords        Define keywords for search engines.
  --markdown        Markdown string.
  --output, -o      Output static pages to the specified directory. Default: "index.html"
  --source, -s      The path of the target file "README.md". Default: "README.md"
  --title           The `<title>` tag is required in HTML documents!
  --version, -v     Show version number
  --help, -h        Displays help information.

Example:

  npm markdown-to-html-cli
  npm markdown-to-html     --title="Hello World!"
  npm markdown-to-html     --config="config/conf.json"
  npm markdown-to-html-cli --markdown="Hello World!"
  npm markdown-to-html-cli --github-corners https://github.com/jaywcjlove/markdown-to-html-cli
  npm markdown-to-html-cli --github-corners https://github.com/jaywcjlove --github-corners-fork
  npm markdown-to-html-cli --output coverage/index.html
  npm markdown-to-html-cli --source README.md
```

## Markdown Features

### Supports for CSS Style

Use HTML comments [`<!--rehype:xxx-->`](https://github.com/jaywcjlove/rehype-attr)<!--rehype:style=color: red;--> to let Markdown support style customization.

```markdown
## Title
<!--rehype:style=display: flex; height: 230px; align-items: center; justify-content: center; font-size: 38px;-->

Markdown Supports **Style**<!--rehype:style=color: red;-->
```

### Support for [GFM footnotes](https://github.blog/changelog/2021-09-30-footnotes-now-supported-in-markdown-fields/)

```markdown
Here is a simple footnote[^1]. With some additional text after it.

[^1]: My reference.
```

### [Task lists](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#task-lists)

To create a task list, preface list items with a regular space character followed by `[ ]`. To mark a task as complete, use `[x]`.

```markdown
- [x] #739
- [ ] https://github.com/octo-org/octo-repo/issues/740
- [ ] Add delight to the experience when all tasks are complete :tada:
```

If a task list item description begins with a parenthesis, you'll need to escape it with `\`:

```markdown
- [ ] \(Optional) Open a followup issue
```

## API

```ts
import { ParsedArgs } from 'minimist';
import { Options } from 'rehype-document';
export interface CreateOptions extends MDToHTMLOptions { }
export declare function create(options?: CreateOptions): string;
export interface RunArgvs extends Omit<ParsedArgs, '_'> {
  version?: string;
  source?: string;
  output?: string;
  /** Add a Github corner to your project page. */
  'github-corners'?: string;
  /** Github corners style. */
  'github-corners-fork'?: boolean;
  /** Markdown string. */
  markdown?: string;
  /** The `<title>` tag is required in HTML documents! */
  title?: string;
  /** Specify the configuration file. Default: `<process.cwd()>/package.json` */
  config?: string;
  /** Define a description of your web page */
  description?: string;
  /** Define keywords for search engines */
  keywords?: string;
  /** Add a Favicon to your Site */
  favicon?: string;
  /** Define the author of a page */
  author?: string;
}
export interface MDToHTMLOptions extends RunArgvs {
  /** [rehype-document](https://github.com/rehypejs/rehype-document#options) options */
  document?: Options;
  /** Rewrite Element. [rehype-rewrite](https://github.com/jaywcjlove/rehype-rewrite#rewritenode-index-parent-void) */
  rewrite?: RehypeRewriteOptions['rewrite'];
  /** rewrite URLs of href and src attributes. */
  reurls?: Record<string, string>;
  /**
   * rehype-wrap Options
   * Wrap selected elements with a given element
   * https://github.com/mrzmmr/rehype-wrap/tree/2402bcdb8ea25bd0948cda72e96d16e65a18c1e9#options
   */
  wrap?: {
    selector?: string;
    wrapper?: string;
  };
}
export declare function run(opts?: Omit<RunArgvs, "_">): any;
export declare const cliHelp: string;
export declare const exampleHelp: string;
```

## Development

```bash
$ npm i
$ npm run build
$ npm run watch
```

## License

MIT © [Kenny Wong](https://wangchujiang.com/)
