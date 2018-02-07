# Linters

In order to utilize the linters provided by this repo, you can use the following commands to import settings into your project.

## [EditorConfig](http://editorconfig.org/)

>helps developers define and maintain consistent coding styles between different editors and IDEs."

[.editorconfig](./.editorconfig)

## [ESLint](https://eslint.org/)

>The pluggable linting utility for JavaScript and JSX

```bash
npm install --save-dev eslint eslint-plugin-import @ciscospark/eslint-config-base
```

**For Projects Using React**

```bash
npm install --save-dev eslint-plugin-react eslint-plugin-jsx-a11y @ciscospark/eslint-config-react
```

### ESLint Base Config
Use this file as a starting point for your project's .eslintrc.
Download [this](./.eslintrc) file, and add rule overrides as needed.

## [stylelint](https://stylelint.io/)

>A mighty, modern CSS linter and fixer that helps you avoid errors and enforce consistent conventions in your stylesheets.

[.stylelintrc.yml](./.stylelintrc.yml)

## [markdownlint](https://github.com/DavidAnson/markdownlint)

>A Node.js style checker and lint tool for Markdown/CommonMark files.

[.markdownlint.json](./.markdownlint.json)
