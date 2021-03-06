# `ws` Code Reading Note

## Protocol Standard
First of all, it is need to clearify that `websocket` protocol is described and defined in `RFC6455`.

https://tools.ietf.org/html/rfc6455

## Code Reading
### `WebSocketServer.js`
1. 426 Upgrade Required
https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/426

> The HTTP 426 Upgrade Required client error response code indicates that the server refuses to perform the request using the current protocol but might be willing to do so after the client upgrades to a different protocol.

2. http.STATUS_CODES
https://nodejs.org/docs/latest/api/http.html#http_http_status_codes

``` node
http.STATUS_CODES[426]
'Upgrade Required'
```

3. server.listen([port][, hostname][, backlog][, callback])

https://nodejs.org/docs/latest/api/http.html#http_server_listen_port_hostname_backlog_callback

> backlog is the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as tcp_max_syn_backlog and somaxconn on linux. The default value of this parameter is 511 (not 512).

4. `Class: http.Server` `Event: 'upgrade'`

https://nodejs.org/docs/latest/api/http.html#http_event_upgrade_1

> Emitted each time a client requests an HTTP upgrade. If this event is not listened for, then clients requesting an upgrade will have their connections closed.

5. `server.close([callback])`

https://nodejs.org/docs/latest/api/http.html#http_server_close_callback

> Stops the server from accepting new connections.

6. `String.prototype.split()`
This method can accept a second parameter which spcified the limitation of result.

> Integer specifying a limit on the number of splits to be found. 

``` javascript
var myString = 'Hello World. How are you doing?';
var splits = myString.split(' ', 3);

console.log(splits);

["Hello", "World.", "How"]
```

7. `request.connection`

https://nodejs.org/docs/latest/api/http.html#http_request_connection

> Reference to the underlying socket. 

8. `TLS (SSL)` and `Class: tls.TLSSocket`

https://nodejs.org/api/tls.html#tls_tls_ssl

> The tls module provides an implementation of the Transport Layer Security (TLS) and Secure Socket Layer (SSL) protocols that is built on top of OpenSSL. 

https://nodejs.org/api/tls.html#tls_class_tls_tlssocket

> The tls.TLSSocket is a subclass of net.Socket that performs transparent encryption of written data and all required TLS negotiation.


`tlsSocket.authorized`
> Returns true if the peer certificate was signed by one of the CAs specified when creating the tls.TLSSocket instance, otherwise false.

`tlsSocket.encrypted`
> Always returns true. This may be used to distinguish TLS sockets from regular net.Socket instances.


9. `Class: net.Socket`

https://nodejs.org/docs/latest/api/net.html#net_class_net_socket

> This class is an abstraction of a **TCP** socket or a streaming **IPC** endpoint (uses named pipes on Windows, and UNIX domain sockets otherwise). A net.Socket is also a **duplex stream**, so it can be both readable and writable, and it is also a **EventEmitter**.

`new net.Socket([options])`
https://nodejs.org/docs/latest/api/net.html#net_new_net_socket_options

options:
  fd
  allowHalfOpen
  readable
  writable

10. `new net.Socket([options]) allowHalfOpen` 

> By default (allowHalfOpen is false) the socket will send a FIN packet back and destroy its file descriptor once it has written out its pending write queue. However, if allowHalfOpen is set to true, the socket will not automatically end() its writable side, allowing the user to write arbitrary amounts of data. The user must call end() explicitly to close the connection (i.e. sending a FIN packet back).


11. `socket.destroy([exception])`

https://nodejs.org/docs/latest/api/net.html#net_socket_destroy_exception

> Ensures that no more I/O activity happens on this socket. Only necessary in case of errors (parse error or so).

> If exception is specified, an 'error' event will be emitted and any listeners for that event will receive exception as an argument.

``` javascript
if (!socket.readable || !socket.writable) return socket.destroy();
```

12. `crypto.createHash(algorithm)`

https://nodejs.org/docs/latest/api/crypto.html#crypto_crypto_createhash_algorithm

> Creates and returns a Hash object that can be used to generate hash digests using the given algorithm.

13. `Class: Hash`

https://nodejs.org/docs/latest/api/crypto.html#crypto_class_hash

> The Hash class is a utility for creating hash digests of data. It can be used in one of two ways:

> As a stream that is both readable and writable, where data is written to produce a computed hash digest on the readable side, or
Using the hash.update() and hash.digest() methods to produce the computed hash.

> The crypto.createHash() method is used to create Hash instances. Hash objects are not to be created directly using the new keyword.

``` javascript
const key = crypto.createHash('sha1')
  .update(req.headers['sec-websocket-key'] + constants.GUID, 'binary')
  .digest('base64');


// offical example
const crypto = require('crypto');
const hash = crypto.createHash('sha256');

hash.update('some data to hash');
console.log(hash.digest('hex'));
// Prints:
//   6a2da20943931e9834fc12cfe5bb47bbd9ae43489a30726962b576f4e3993e50
```

`hash.update(data[, inputEncoding])`

> Updates the hash content with the given data, the encoding of which is given in inputEncoding and can be 'utf8', 'ascii' or 'latin1'. If encoding is not provided, and the data is a string, an encoding of 'utf8' is enforced. If data is a Buffer, TypedArray, or DataView, then inputEncoding is ignored.

`hash.digest([encoding])`

> Calculates the digest of all of the data passed to be hashed (using the hash.update() method). The encoding can be 'hex', 'latin1' or 'base64'. If encoding is provided a string will be returned; otherwise a Buffer is returned.


14. `Array.prototype.reduce()`

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce

> The reduce() method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

`arr.reduce(callback[, initialValue])
`

`callback` takes four parameters:
`accumulator`, `currentValue`, `currentIndex` and `array`.

``` javascript
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(function(a, b) {
  return a.concat(b);
}, []);
// flattened is [0, 1, 2, 3, 4, 5]
```


15. `emitter.emit(eventName[, ...args])`
https://nodejs.org/docs/latest/api/events.html#events_emitter_emit_eventname_args

> Synchronously calls each of the listeners registered for the event named eventName, in the order they were registered, passing the supplied arguments to each.

> Returns `true` if the event had listeners, `false` otherwise.


16. `socket.write(data[, encoding][, callback])`

> Returns `true` if the entire data was flushed successfully to the kernel buffer. Returns `false` if all or part of the data was queued in user memory. `'drain'` will be emitted when the buffer is again free.

``` javascript
socket.write(headers.concat('', '').join('\r\n'));
```

17. `emitter.removeListener(eventName, listener)`

https://nodejs.org/docs/latest/api/events.html#events_emitter_removelistener_eventname_listener

> Removes the specified listener from the listener array for the event named eventName.

> removeListener will remove, **at most, one instance of a listener** from the listener array. If any single listener has been added multiple times to the listener array for the specified eventName, then removeListener must be called multiple times to remove each instance.