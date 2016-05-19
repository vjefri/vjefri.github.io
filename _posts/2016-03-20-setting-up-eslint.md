---
layout: post
title:  "Setting Up ESlint"
date:   2016-03-20 21:28:15 +0700
categories: [JavaScript]
---

# Setting Up ESLINT
ESLint is the pluggable linter utility for JavaScript and JSX. What separates ESLint from other linters like JSHint is its pluggable nature. You can find plugins on npm by searching `eslintplugin`. 

You can install ESLint using npm:
`npm install -g eslint`

Before you install ESLint make sure to uninstall other linters you might have installed. I haven’t tested two linters working together, so it’s best to remove the other linters. 

Check what you have installed via npm : `npm list -g --depth=0`
Uninstall: `npm uninstall -g [name (ex. jshint)]`

## Configuring Sublime
Install SublimeLinter package via Package Control. If you do not see it, you might already have it installed. Don’t know about Package Control? [Read this]. [SublimeLinter] is a framework for linters. You can tell it to work with ESLint by installing the following package via package control: `SublimeLinter-contrib-eslint`. Remember to [remove] any other linters you have installed with SublimeLinter. 

## Configuring Atom
In terminal type `apm install linter` and `apm install linter-eslint`.

## Plugins
As mentioned previously, one of ESLint’s original goals was to enable developers to write their own custom rules and plug them in at runtime. 

`npm install eslint-plugin-react --save-dev`

Then, in your configuration file, you indicate that `eslint-plugin-react` should be loaded by using the plugins array. 


```javascript
{
  "parserOptions": {
	"ecmaFeatures": {
	  "jsx": true
	}
  },
  "env": {
	"es6": true
  },
  "plugins": [
	"react" // you can just say “react”
  ]
}
```