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







