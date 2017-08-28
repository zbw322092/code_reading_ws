# Differences between TCP sockets and web sockets
1. Differences between TCP sockets and web sockets, one more time
https://stackoverflow.com/questions/16945345/differences-between-tcp-sockets-and-web-sockets-one-more-time

- `WebSocket` is basically an `application protocol` (with reference to the ISO/OSI network stack), **message-oriented**, which **makes use of TCP as transport layer**.

Detailed explantion:
https://stackoverflow.com/a/26365415


2. What is the fundamental difference between WebSockets and pure TCP?
- Over the internet, you're communicating with someone else's server on the other end. They are extremely unlikely to have any old socket open for connections. Usually they will have only a few standard ones such as port `80` for HTTP or `443` for HTTPS. So, to communicate with the server you are obliged to connect using one of those ports.

Detailed explantion:
https://stackoverflow.com/a/2681874


3. WebSocket wikipedia
https://en.wikipedia.org/wiki/WebSocket

- WebSocket is a **computer communications protocol**, providing **full-duplex** communication channels over a single **TCP connection**.

- WebSocket is designed to be implemented in web browsers and web servers, but it can be used by any client or server application. The WebSocket Protocol is **an independent TCP-based protocol**. Its only relationship to HTTP is that its handshake is interpreted by HTTP servers as an `Upgrade` request.


