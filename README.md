## Emit với SocketServer | API SERVER


## Emit cheatsheet

```js

io.on('connect', onConnect);

function onConnect(socket){

  // gửi đến 1 client
  socket.emit('hello', 'can you hear me?', 1, 2, 'abc');

  // gửi cho tất cả mọi người | ngoại trừ người gửi
  socket.broadcast.emit('broadcast', 'hello friends!');

  // gửi cho tất cả mọi người trong 1 room | trừ người gửi
  socket.to('game').emit('nice game', "let's play a game");

  // gửi cho tất cả mọi người trong room game1 vs game2 | trừ người gửi
  socket.to('game1').to('game2').emit('nice game', "let's play a game (too)");

  // gửi cho tất cả mọi người trong 1 room | chứa luôn người gửi
  io.in('game').emit('big-announcement', 'the game will start soon');

 // gửi cho tất cả mọi người trong 1 namespace | chứa luôn người gửi
  io.of('myNamespace').emit('bigger-announcement', 'the tournament will start soon');

  // gửi cho tất cả mọi người trong 1 room và room thuộc 1 namespace | chứa luôn người gửi
  io.of('myNamespace').to('room').emit('event', 'message');

  // gửi đến 1 user(socketID)
  io.to(<socketid>).emit('hey', 'I just met you');

  // sending with acknowledgement
  socket.emit('question', 'do you think so?', function (answer) {});

  // sending without compression
  socket.compress(false).emit('uncompressed', "that's rough");

  // gửi một tin nhắn có thể bị xóa nếu máy khách(client=socketID) chưa sẵn sàng nhận tin nhắn
  socket.volatile.emit('maybe', 'do you really need it?');

  // Xác định liệu dữ liệu để gửi có dữ liệu nhị phân hay không
  socket.binary(false).emit('what', 'I have no binaries!');

  // gửi cho tất cả các máy khách trên nút này (khi sử dụng nhiều nút)
  io.local.emit('hi', 'my lovely babies');

  // gửi cho tất cả client đã kết nối
  io.emit('an event sent to all connected clients');

};

```

**Note:** Các sự kiện sau được dành riêng và không nên được sử dụng làm tên sự kiện theo ứng dụng của bạn:
- `error`
- `connect`
- `disconnect`
- `disconnecting`
- `newListener`
- `removeListener`
- `ping`
- `pong`

**SERVER API**
- https://github.com/socketio/socket.io/blob/master/docs/API.md#new-serverhttpserver-options

**CLIENT API**
- https://github.com/socketio/socket.io-client/blob/master/docs/API.md

