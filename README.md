# Errors-Guide

This is a small guide to some of the most common errors that we can encounter during the BootCamp or our work.

**Index**   

- [FrontEnd](#frontend)
- [BackEnd (Express, MySQL, Sequelize)](#BackEnd)
  - [Address already in use](#address-already-in-use)
  - [Cannot find module](#cannot-find-module)
  - [Acces denied](#acces-denied)
  - [ConnectionRefusedError](#connectionrefusedError)
- [FrontEnd (React JS)](#frontend)



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

This error occurs when Node.js cannot find the specified module in your code. In this case, the error message indicates that it cannot find the ```'../models/members.model.js'``` module that is being required in your 'auth.controller.js' file.

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
### Acces denied

```bash
/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/mysql/connection-manager.js:94
          throw new SequelizeErrors.AccessDeniedError(err);
                ^

AccessDeniedError [SequelizeAccessDeniedError]: Access denied for user 'userName'@'localhost' (using password: YES)
    at ConnectionManager.connect (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/mysql/connection-manager.js:94:17)
    at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
    at async ConnectionManager._connect (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/abstract/connection-manager.js:222:24)
    at async /Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/abstract/connection-manager.js:174:32
    at async ConnectionManager.getConnection (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/abstract/connection-manager.js:197:7)
    at async /Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/sequelize.js:305:26
    at async Sequelize.authenticate (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/sequelize.js:457:5)
    at async checkConnection (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/database/index.js:17:9)
    at async checkAndSyncMySQL (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/index.js:25:11)
    at async startAPI (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/index.js:36:11) {
  parent: Error: Access denied for user 'userName'@'localhost' (using password: YES)
      at Packet.asError (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/packets/packet.js:728:17)
      at ClientHandshake.execute (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/commands/command.js:29:26)
      at Connection.handlePacket (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/connection.js:478:34)
      at PacketParser.onPacket (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/connection.js:97:12)
      at PacketParser.executeStart (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/packet_parser.js:75:16)
      at Socket.<anonymous> (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/connection.js:104:25)
      at Socket.emit (node:events:514:28)
      at addChunk (node:internal/streams/readable:343:12)
      at readableAddChunk (node:internal/streams/readable:316:9)
      at Readable.push (node:internal/streams/readable:253:10) {
    code: 'ER_ACCESS_DENIED_ERROR',
    errno: 1045,
    sqlState: '28000',
    sqlMessage: "Access denied for user 'userName'@'localhost' (using password: YES)",
    sql: undefined
  },
  original: Error: Access denied for user 'userName'@'localhost' (using password: YES)
      at Packet.asError (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/packets/packet.js:728:17)
      at ClientHandshake.execute (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/commands/command.js:29:26)
      at Connection.handlePacket (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/connection.js:478:34)
      at PacketParser.onPacket (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/connection.js:97:12)
      at PacketParser.executeStart (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/packet_parser.js:75:16)
      at Socket.<anonymous> (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/mysql2/lib/connection.js:104:25)
      at Socket.emit (node:events:514:28)
      at addChunk (node:internal/streams/readable:343:12)
      at readableAddChunk (node:internal/streams/readable:316:9)
      at Readable.push (node:internal/streams/readable:253:10) {
    code: 'ER_ACCESS_DENIED_ERROR',
    errno: 1045,
    sqlState: '28000',
    sqlMessage: "Access denied for user 'userName'@'localhost' (using password: YES)",
    sql: undefined
  }
}
```
This error message indicates an "Access Denied" error when trying to establish a connection to a MySQL database using Sequelize. The error message Access denied for user 'userName'@'localhost' (using password: YES) suggests that the MySQL server denied access to the specified user with the given password.
Here's what you can do to resolve this issue:

- **Check Database Credentials:** double-check the username and password specified in your Sequelize configuration file. Ensure they are correct and have the necessary permissions to access the database.
- **Verify MySQL User Privileges:** log in to your MySQL server using a MySQL client or a tool like phpMyAdmin.
Check if the user 'userName' has the necessary privileges to connect to the database. If not, grant the required privileges using the following SQL command:
```mysql
GRANT ALL PRIVILEGES ON *.* TO 'userName'@'localhost' IDENTIFIED BY 'password';
```
Replace database_name with the actual name of your database, and ensure that 'userName' and 'password' match the credentials in your Sequelize configuration.

- **Check Network Restrictions:** if you're trying to connect to a remote MySQL server, make sure that the server allows connections from your IP address. You might need to configure the MySQL server to accept remote connections or adjust firewall settings.
- **Verify MySQL Server Status:** ensure that your MySQL server is up and running. Sometimes, connection issues occur when the MySQL server is not running or is misconfigured.
**Check for Typos:** carefully check your Sequelize configuration and ensure there are no typos in the database name, username, or password.
- **Database Host Configuration:** verify that the host configuration in your Sequelize setup is correct. If the MySQL server is on the same machine, 'localhost' is the correct host. If it's a remote server, use the server's IP address or domain name.
- **Temporary Disable Firewall/Antivirus:** in some cases, firewall or antivirus software might block the connection. Temporarily disable them and check if the issue persists.
- **Database Server Logs:** check MySQL server logs for any additional error messages or details about the connection attempt. MySQL error logs can provide valuable information.

### ConnectionRefusedError

```bash
/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/mysql/connection-manager.js:92
          throw new SequelizeErrors.ConnectionRefusedError(err);
                ^

ConnectionRefusedError [SequelizeConnectionRefusedError]
    at ConnectionManager.connect (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/mysql/connection-manager.js:92:17)
    at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
    at async ConnectionManager._connect (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/abstract/connection-manager.js:222:24)
    at async /Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/abstract/connection-manager.js:174:32
    at async ConnectionManager.getConnection (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/dialects/abstract/connection-manager.js:197:7)
    at async /Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/sequelize.js:305:26
    at async Sequelize.authenticate (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/node_modules/sequelize/lib/sequelize.js:457:5)
    at async checkConnection (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/database/index.js:17:9)
    at async checkAndSyncMySQL (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/index.js:25:11)
    at async startAPI (/Users/cex/Desktop/AfricandotoV2/BackEnd/AfricanDoto.v2/index.js:36:11) {
  parent: AggregateError
      at internalConnectMultiple (node:net:1114:18)
      at afterConnectMultiple (node:net:1667:5) {
    code: 'ECONNREFUSED',
    fatal: true,
    [errors]: [
      Error: connect ECONNREFUSED ::1:2345
          at createConnectionError (node:net:1634:14)
          at afterConnectMultiple (node:net:1664:40) {
        errno: -61,
        code: 'ECONNREFUSED',
        syscall: 'connect',
        address: '::1',
        port: 2345
      },
      Error: connect ECONNREFUSED 127.0.0.1:2345
          at createConnectionError (node:net:1634:14)
          at afterConnectMultiple (node:net:1664:40) {
        errno: -61,
        code: 'ECONNREFUSED',
        syscall: 'connect',
        address: '127.0.0.1',
        port: 2345
      }
    ]
  },
  original: AggregateError
      at internalConnectMultiple (node:net:1114:18)
      at afterConnectMultiple (node:net:1667:5) {
    code: 'ECONNREFUSED',
    fatal: true,
    [errors]: [
      Error: connect ECONNREFUSED ::1:2345
          at createConnectionError (node:net:1634:14)
          at afterConnectMultiple (node:net:1664:40) {
        errno: -61,
        code: 'ECONNREFUSED',
        syscall: 'connect',
        address: '::1',
        port: 2345
      },
      Error: connect ECONNREFUSED 127.0.0.1:2345
          at createConnectionError (node:net:1634:14)
          at afterConnectMultiple (node:net:1664:40) {
        errno: -61,
        code: 'ECONNREFUSED',
        syscall: 'connect',
        address: '127.0.0.1',
        port: 2345
      }
    ]
  }
}
```

This error message indicates that your application attempted to connect to a MySQL database, but the connection was refused by the MySQL server. Let me break down the error message for you:

```bash
ConnectionRefusedError [SequelizeConnectionRefusedError]
```
This line indicates that a Sequelize connection to the MySQL database was attempted, but the connection was refused by the server.

```bash
Error: connect ECONNREFUSED ::1:2345
Error: connect ECONNREFUSED 127.0.0.1:2345
```

These lines show the specific connection errors. The ECONNREFUSED error means that the connection was actively refused by the target machine. In this case, your application tried to connect to the MySQL server on ::1 (IPv6 loopback address) and 127.0.0.1 (IPv4 loopback address) at port 2345, but the MySQL server refused the connection.

Here are a few steps you can take to troubleshoot and resolve this issue:

- **Check MySQL Server Status:** ensure that your MySQL server is up and running. If it's not running, start the server. You can check the status of your MySQL server using a command like mysqladmin status in the terminal.

- **Verify MySQL Server Port:** double-check that your MySQL server is configured to listen on the port 2345. If your MySQL server is configured to use a different port, update your Sequelize configuration to use the correct port number.

- **Check Firewall Settings:** make sure that your firewall allows connections to port 2345. If you are running a firewall on your server, configure it to allow incoming connections on the MySQL port.

- **Check MySQL Bind Address:** check your MySQL server configuration file (usually my.cnf or my.ini) and ensure that MySQL is configured to listen on the correct network interface (::1 and 127.0.0.1 for loopback, or a specific IP address for external connections).

- **Check Other Processes:** ensure that there are no other applications or processes already using port 2345 on your server. You can check for open ports using the netstat or lsof command.

- **Database User Permissions:** verify that the user specified in your Sequelize configuration has permission to connect from the specified host (::1 and 127.0.0.1). If not, grant the necessary privileges to the user.

- **Restart Your Application:** sometimes, issues can be resolved by simply restarting your application after making configuration changes.

By carefully reviewing your MySQL server configuration, firewall settings, and ensuring that your application's connection details are correct, you should be able to resolve the "Connection Refused" error and successfully connect to your MySQL database.



## FrontEnd
