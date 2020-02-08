# crypto

## Need crypto below 
* Protecting password 
* Protecting data at rest 
* Data transit 
* Two factor authentication


### Protecting password 

#### Hashing 

* MD5 - Message digest 

```js 
const crypto = require('crypto');
const hash = crypto.createHash('md5');
hash.update('<Password>');
hash.digest('hex');
```

* sha256 - Secure Hash Algorithm  

```js 
const crypto = require('crypto');
const hash = crypto.createHash('sha256');
hash.update('<Password>');
hash.digest('hex');
```

* Argon2 
* PBKDF2 - Password-Based Key Derivation Function 2

```js
const crypto = require('crypto');
const password = '<password>'
const salt = crypto.randomBytes('sha256').toString('hex');
const hashed = crypto.pdkdf2Sync(password, salt, 100000, 512, 'sha512')
hashed.toString('hex');
```
* scrypt
* bcrypt





## Usefull link:

* https://haveibeenpwned.com/
* https://hashtoolkit.com/
* https://hunter2.com/zero-to-hashing-in-under-10-minutes-argon2-in-nodejs
