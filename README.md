# chokidar-socket-emitter
a simple chokidar watcher and socket.io server which emits file system events to all connected socket.io clients. Primarily it should serve as an event source for **[systemjs-hot-reloader](https://github.com/capaj/systemjs-hot-reloader)** but you can use it any other way.

## Install
```
npm i -D chokidar-socket-emitter
```

## CLI usage

```
npm i -g chokidar-socket-emitter
chokidar-socket-emitter -l 1234
```

By default listens on port 5776.

## NPM script usage
Combined with [browser-sync](https://browsersync.io/):

``` json
"scripts": {
  "start": "npm run serve & npm run watch",
  "serve": "browser-sync start --server",
  "watch": "chokidar-socket-emitter"
},
```
Start by running:
```
npm start
```

## Programatic usage
```javascript
var chokidarEvEmitter = require('chokidar-socket-emitter')
chokidarEvEmitter({port: 8090}) //path is taken from jspm/directories/baseURL or if that is not set up, '.' is used
//or specify the path
chokidarEvEmitter({port: 8090, path: '.'})

//you can also supply a http server instance, that way it will run within your server, no need for extra port
require('chokidar-socket-emitter')({app: server})  

//you can also supply an io server instance
require('chokidar-socket-emitter')( { io: my.io } ) 
```

## FAQ

#### Does chokidar have problems with watching drives mounted from VMs hosts/network?
Yes and if you want it to work, use additional opts property to switch to polling mode
```
chokidarEvEmitter({port: 8090, path: '.', chokidar: {usePolling: true}})
```

