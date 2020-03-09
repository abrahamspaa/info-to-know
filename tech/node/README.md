# Node.js

V8 and libuv

## Node VMs

- V8 (node REPL -> process.versions.v8)
 - Shipping
 - Stable (Not yet release, Ex: node --harmony)
 - In progress (node --v8-options | grep "in progress")
- Chakra 

## How node works

- Node user v8 via v8 C++ API
- Node as it own Core Modules api (Ex: timmer, network.. etc)
- C++ Binding 
- Node uses async opration via libuv (C libary for nodejs )
- Http-parser
- c-ares (async DNS query)
- openSSL (Crypto)
- zlib

How required module works?

- Resolving (Finding the file)
- Loading (Content of the file)
- Wrapping 
- Evaluating 
- Caching


require.cache - for cache code which export

## Commond 

- node -p "os.cpus()" - What and number of processor running? 
- node -p "process.arch" - What archtecture system running
- 
