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
const password = '<password>';
const salt = crypto.randomBytes('sha256').toString('hex');
const hashed = crypto.pdkdf2Sync(password, salt, 100000, 512, 'sha512')
hashed.toString('hex');
```
* scrypt
* bcrypt


### Protecting data at rest 

#### Symmetric Encryption

Steps 
- one key 
- Makes data unreadable

```js
// Encrypt
const crypto = require('crypto');
const algorithm = 'aes-256-cbc';
const password = '<password>';
const salt = crypto.randomBytes('32');
const key = crypto.pdkdf2Sync(password, salt, 32);
const iv = crypto.randomBytes(16);
const cipher = crypto.createCipheriv(algorithm, key, iv);

let text = <text>;
let encrypted = cipher.update(text, 'utf8', 'hex');

encrypted += cipher.final('hex');

// Decrypt 
const decipher = crypto.createDecipheriv(algorithm, key, iv);

let decrypted = decipher.update(encrypted, 'hex', 'utf8');
```
#### vault

### Protecting data in Transit 

#### Asymmetric Encryption

```js
// Encrypt
const crypto = require('crypto');
const user1 = crypto.createDiffieHellman(2048);
const user1key = user1.generateKeys();

const user2 = crypto.createDiffieHellman(user1.getPrime(), user1.getGenerator());
const user2Key = user2.generateKeys();

const user1Secret = user1.computeSecret(user2key);
const user2Secret = user2.computeSecret(user1key);

console.log(user1Secret.toString('hex'));
console.log(user2Secret.toString('hex'));
```

#### HMAC - document is not change

```js
// Encrypt
const crypto = require('crypto');
const hmac = crypto.createHmac('sha256', 'a secret');

hmac.update('date to protect');
console.log(hmac.digest('hex')); // this document between user1 and user2 should be same 
```

### Two factor Authentication 

Factor ?

- Password 
- Token or ID card or soft token 
- Biometrics 
- One Time Password (OTP) ( Speak Easy Lib)





# Real Time 

- For Login user use two factor authentication 
- For Application server use Asymmetric Encryption (Public and private key)
- For Data Base use symmetric Encryption (Key store)



## Usefull link:

* https://haveibeenpwned.com/
* https://hashtoolkit.com/
* https://hunter2.com/zero-to-hashing-in-under-10-minutes-argon2-in-nodejs
* https://justinboyerwriter.com/2017/07/29/developers-guide-cryptography-basics/


## Example:

- NodeGoat - https://github.com/OWASP/NodeGoat

