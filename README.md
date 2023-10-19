# Errors-Guide

This is a small guide to some of the most common errors that we can encounter during the BootCamp or our work.

**Index**   

- [FrontEnd](#frontend)
- [BackEnd](#BackEnd)
  - [Address already in use](#address-already-in-use)
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





## FrontEnd
