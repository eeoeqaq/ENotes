服务器如何向客户端传递信息？
客户端主动向服务器搭建sockets，服务器管理sockets并利用他们回传信息
```js
socketsServer.getIo().emit(channelName, data);
socket.on(channelName, callbackFunc);
```