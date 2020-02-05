# Command Line Interface (CLI)

Do a thing and do it well. Processes commands to a computer program in the form of lines of text.

# Step to build 

* npm init -y
* create `bin` folder and script file <sample.js> (with systax at the top `#! /usr/bin/env node`)
* in package.json add below, this is called sheband syntax 
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

Note: this file will be Store on home directory with dot before directory

# Config or own setting

User below 
* npm configstore and inquire


