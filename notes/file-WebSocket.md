# `WebSocket.js`
1. `socket.bufferSize`

https://nodejs.org/docs/latest/api/net.html#net_socket_buffersize

> ... Node.js will internally queue up the data written to a socket and send it out over the wire when it is possible. (Internally it is polling on the socket's file descriptor for being writable)...

2. `socket.setTimeout(timeout[, callback])`

https://nodejs.org/docs/latest/api/net.html#net_socket_settimeout_timeout_callback

> Sets the socket to timeout after timeout milliseconds of inactivity on the socket. By default net.Socket do not have a timeout.

> When an idle timeout is triggered the socket will receive a 'timeout' event but the connection will not be severed. The user must manually call socket.end() or socket.destroy() to end the connection.

``` javascript
socket.setTimeout(3000);
socket.on('timeout', () => {
  console.log('socket timeout');
  socket.end();
});

socket.setTimeout(0);
```

> If timeout is 0, then the existing idle timeout is disabled.

3. `socket.setNoDelay([noDelay])`

https://nodejs.org/docs/latest/api/net.html#net_socket_setnodelay_nodelay

> Disables the Nagle algorithm. By default TCP connections use the Nagle algorithm, they buffer data before sending it off. Setting true for noDelay will immediately fire off data each time socket.write() is called. noDelay defaults to `true`.

4. `Array.prototype.unshift()`

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift

> The unshift() method adds one or more elements to the beginning of an array and returns the new length of the array.



5. `readable.unshift(chunk)`

https://nodejs.org/docs/latest/api/stream.html#stream_readable_unshift_chunk

> The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.


https://stackoverflow.com/questions/29072331/putting-data-back-onto-a-readable-stream

``` javascript
if (head.length > 0) socket.unshift(head);
```

6. `socket.end([data][, encoding])`

https://nodejs.org/docs/latest/api/net.html#net_socket_end_data_encoding

> Half-closes the socket. i.e., it sends a FIN packet. It is possible the server will still send some data.

> If data is specified, it is equivalent to calling `socket.write(data, encoding)` followed by `socket.end()`.

`socket.destroy([exception])` Only necessary in case of errors.
> Ensures that no more I/O activity happens on this socket. Only necessary in case of errors (parse error or so).

https://nodejs.org/docs/latest/api/net.html#net_socket_destroy_exception

``` javascript
if (!error) 
  this._socket.end();
else 
  this._socket.destroy();
```

7. `socket.pause()`

https://nodejs.org/docs/latest/api/net.html#net_socket_pause

> Pauses the reading of data. That is, 'data' events will not be emitted. Useful to throttle back an upload.

8. `socket.resume()`

https://nodejs.org/docs/latest/api/net.html#net_socket_resume

> Resumes reading after a call to socket.pause().

9. `request.abort()`

https://nodejs.org/docs/latest/api/http.html#http_request_abort

> Marks the request as aborting. Calling this will cause remaining data in the response to be dropped and the socket to be destroyed.



10. `request.aborted`

https://nodejs.org/docs/latest/api/http.html#http_request_aborted

> If a request has been aborted, this value is the time when the request was aborted, in milliseconds since 1 January 1970 00:00:00 UTC.

11. `emitter.listeners(eventName)`

https://nodejs.org/docs/latest/api/events.html#events_emitter_listeners_eventname

> Returns a copy of the array of listeners for the event named eventName.

12. `http.request(options[, callback])`

https://nodejs.org/docs/latest/api/http.html#http_http_request_options_callback


options
  > `localAddress`  Local interface to bind for network connections.

Stackoverflow:
https://stackoverflow.com/questions/20294190/send-http-request-from-different-ips-in-node-js

> In the node http module there is a localAddress option for binding to specific network interface.

``` javascript
var http = require('http');

var options = {
  hostname: 'www.example.com',
  localAddress: '202.1.1.1'
};

var req = http.request(options, function(res) {
  res.on('data', function (chunk) {
    console.log(chunk.toString());
  });
});
```

option
> `family` IP address family to use when resolving host and hostname. Valid values are 4 or 6. When unspecified, both IP v4 and v6 will be used.

option
> `socketPath`  Unix Domain Socket (use one of host:port or socketPath).

option
> `socketPath`  Unix Domain Socket (use one of host:port or socketPath).


13. `https.request(options[, callback])`

https://nodejs.org/docs/latest/api/https.html#https_https_request_options_callback

> additional options from tls.connect() are also accepted when using a custom `Agent`: `pfx`, `key`, `passphrase`, `cert`, `ca`, `ciphers`, `rejectUnauthorized`, `secureProtocol`, `servername`

14. `tls.connect(options[, callback])`

https://nodejs.org/api/tls.html#tls_tls_connect_options_callback


15. `Class: http.Agent`

https://nodejs.org/docs/latest/api/http.html#http_class_http_agent

> An `Agent` is responsible for managing connection persistence and reuse for **HTTP clients**. It maintains a queue of pending requests for a given host and port, **reusing a single socket connection** for each until the queue is empty, at which time the socket is either destroyed or put into a **pool** where it is kept to be used again for requests to the same host and port. Whether it is destroyed or pooled depends on the `keepAlive` option.