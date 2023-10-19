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
Finally we can start our server with ```nodemon``` or ```node --watch index.js```.





## FrontEnd
