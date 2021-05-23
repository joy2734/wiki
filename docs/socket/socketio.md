# Socket IO

## Socket IO
 - 양방향 커뮤니케이션 통신을 제공 client와 서버사이에
 - 서버는 클라이언트에게 push로 메세지를 보내줌
 - 소켓 io는 두가지 part로 구성됨
    - Node.JS HTTP Server socket.io 와 통합 (또는 마운트)하는 서버
    - 브라우저 측 socket.io-client 에로드되는 클라이언트 라이브러리

 - 코드
  - 
```javascript
    const express = require('express');
    const app = express();
    const http = require('http');
    const server = http.createServer(app);
    const { Server } = require("socket.io");
    const io = new Server(server);

    app.get('/', (req, res) => {
    res.sendFile(__dirname + '/index.html');
    });

    io.on('connection', (socket) => {
    console.log('a user connected');
    });

    server.listen(3000, () => {
    console.log('listening on *:3000');
    });

```

## Emitting events

- SocketIO의 main idea는 원하는 어느 데이터나 이벤트를 주고 받는것이다. json이나 binary데이터로.
- 유저가 메세지를 적을때 서버는 `chat Message` 이벤트를 가져온다.
- js상에 socket emit이벤트를 발생시 node 서버에서 socket

```javascript

//index.html
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io();

  var form = document.getElementById('form');
  var input = document.getElementById('input');

  form.addEventListener('submit', function(e) {
    e.preventDefault();
    if (input.value) {
      socket.emit('chat message', input.value);
      input.value = '';
    }
  });


  //node 서버

  io.on('connection', (socket) => {
  socket.on('chat message', (msg) => {
    console.log('message: ' + msg);
  });
});
</script>
```

## Broadcasting

 - 서버로부터 나머지유저에게 emit 메세지를 전달.
 - io.emit사용

 ```javascript
   io.on('connection', (socket) => {
  socket.on('chat message', (msg) => {
    io.emit('chat message', msg)
  });
 ```

 ## homeWork진행
 - 누군가 접속하거나 끊겻을떄 메세지를보여준다.(방입장, 퇴장)
 - 닉네임추가
 - 누가온라인인지 보여주기
 - private 메세지추가??
 - 사용자가 입력중입니다. 기능추가(맨밑에추가)


