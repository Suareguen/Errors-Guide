# Errors-Guide

This is a small guide to some of the most common errors that we can encounter during the BootCamp or our work.

**Index**   

- [FrontEnd](#frontend)
- [BackEnd](#BackEnd)
  - [Address already in use](#address-already-in-use)
  - [Cannot find module](#cannot-find-module)
- [FrontEnd](#frontend)



## Javascript


## BackEnd

### Address already in use

```bash
node:events:492
      throw er; // Unhandled 'error' event
      ^

Error: listen EADDRINUSE: address already in use :::3000
    at Server.setupListenHandle [as _listen2] (node:net:1872:16)
    at listenInCluster (node:net:1920:12)
    at Server.listen (node:net:2008:7)
    at Function.listen (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/express/lib/application.js:635:24)
    at initializeAndListenWithExpress (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/index.js:15:8)
    at startAPI (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/index.js:37:11)
    at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
Emitted 'error' event on Server instance at:
    at emitErrorNT (node:net:1899:8)
    at process.processTicksAndRejections (node:internal/process/task_queues:82:21) {
  code: 'EADDRINUSE',
  errno: -48,
  syscall: 'listen',
  address: '::',
  port: 3000
}
```

This error usually occurs because we are trying to start our server, but it is already running in another location (another terminal window that we have open) or because we did not close the connection properly. To solve this problem, first, check if the server is running elsewhere, if not, enter the following commands in the terminal:
```bash
lsof -i :3000
```

If everything it´s ok you should see this: 
```
COMMAND  PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
node    6824  cex   24u  IPv6 0x409d2d698870de01      0t0  TCP *:hbci (LISTEN)
```
And now we copy the the PID number, in this example 6824, and type in the terminal:
```bash
kill -9 <PID number>
```
Example:
```bash
kill -9 6824
```
Finally we can start our server with ```nodemon``` or ```node --watch index.js```.

### Cannot find module
```bash
node:internal/modules/cjs/loader:1048
  const err = new Error(message);
              ^

Error: Cannot find module '../models/members.model.js'
Require stack:
- /Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/api/controllers/auth.controller.js
- /Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/api/routes/auth.router.js
- /Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/api/routes/index.js
- /Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/index.js
    at Module._resolveFilename (node:internal/modules/cjs/loader:1048:15)
    at Module._load (node:internal/modules/cjs/loader:901:27)
    at Module.require (node:internal/modules/cjs/loader:1115:19)
    at require (node:internal/modules/helpers:130:18)
    at Object.<anonymous> (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/api/controllers/auth.controller.js:1:16)
    at Module._compile (node:internal/modules/cjs/loader:1233:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1287:10)
    at Module.load (node:internal/modules/cjs/loader:1091:32)
    at Module._load (node:internal/modules/cjs/loader:938:12)
    at Module.require (node:internal/modules/cjs/loader:1115:19) {
  code: 'MODULE_NOT_FOUND',
  requireStack: [
    '/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/api/controllers/auth.controller.js',
    '/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/api/routes/auth.router.js',
    '/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/api/routes/index.js',
    '/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/index.js'
  ]
}
```

This error occurs when Node.js cannot find the specified module in your code. In this case, the error message indicates that it cannot find the '../models/members.model.js' module that is being required in your 'auth.controller.js' file.

To solve this problem, you can follow these steps:
- **Verify the module path:** Make sure the path to the 'members.model.js' file is correct. Ensure that the file actually exists at the specified location and that the path is correct in your code.

- **Check spelling and case:** File systems on some operating systems are case-sensitive. Ensure that the spelling and letter case in the file path exactly match the file name and folder structure on your file system.

- **Review module references:** Double-check that you are requiring the module in the correct file. In this case, the error seems to be occurring in 'auth.controller.js', so ensure that the line of code requiring the module has the correct path and does not have any typographical errors.

- **Ensure the file is not corrupted or empty:** Sometimes, files can get corrupted or accidentally become empty, leading to these types of errors. Open the 'members.model.js' file and check that the code is intact and not empty.

- **Reinstall dependencies:** If everything else seems correct and you are still experiencing the error, try reinstalling your project's dependencies. This can resolve issues related to installation or missing dependencies.

To reinstall the dependencies, open a terminal in your project directory and run the following command:
```bash
npm i
```




## FrontEnd
