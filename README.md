# Errors-Guide

**Índice**   
1. [Javascript](#id1)
2. [BackEnd](#id2)
3. [FrontEnd](#id3)

## Javascript<a name="id1"></a>


## BackEnd<a name="id2"></a>

### address already in use :::3000<a name="sub2"></a>
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


## FrontEnd<a name="id3"></a>
