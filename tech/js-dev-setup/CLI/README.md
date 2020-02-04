# Command Line Interface (CLI)

Do a thing and do it well. Processes commands to a computer program in the form of lines of text.

# Step to build 

* npm init -y
* create `bin` folder and script file <sample.js> (with systax at the top `#! /usr/bin/env node`)
* in package.json add below 
```js
bin: {
  sample: './bin/sample'
}
```
* For dev we can use `npm link`
* and run `sample`

# File formate to store data

* INI
* JSON
* XML

Note: Store this file in home directory with dot before directory
