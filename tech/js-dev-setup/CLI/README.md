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


# Store Username or credential

npm -> keytar-prebuild

# options and commands 

npm -> commander

# Folder Structure 

* CLI command -> bin dir 
* code implmeneted -> commands dir
* command user function -> lib dir

# Error 


* process.stdin -> standard in
* process.stdout -> standard out
* process.stderr -> standard error 



Example: https://github.com/pofallon/twine/tree/master

