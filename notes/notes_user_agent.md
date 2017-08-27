# User Agent

1. What's My User Agent?

http://www.whoishostingthis.com/tools/user-agent/

> Everyone that is browsing the web right now has a user agent. It's the software that acts as the bridge between you, the user, and the internet.

2. Node.js `HTTP Agent` Class
2.1

http://www.apetuts.com/tutorial/node-js-http-agent-class/

> ... A http agent is used by a client to **group or pool sockets**. A http agent helps in managing http client request sockets efficiently.

> The `http.Agent` class contains the required properties and functions to perform operations on http agents.

> The http agents are especially useful when multiple sockets are kept alive...

> ... All client request sockets are pooled into a http globalAgent by default.

2.2
https://nodejs.org/docs/latest/api/http.html#http_class_http_agent

> An Agent is responsible for **managing connection persistence and reuse for HTTP clients**. It maintains a queue of pending requests for a given host and port, reusing a single socket connection for each until the queue is empty, at which time the socket is either destroyed or put into a pool where it is kept to be used again for requests to the same host and port. Whether it is destroyed or pooled depends on the keepAlive option...

2.3
`new Agent([options])`

https://nodejs.org/docs/latest/api/http.html#http_new_agent_options








3. `http.globalAgent`

https://nodejs.org/docs/latest/api/http.html#http_http_globalagent

> Global instance of Agent which is used as the default for all HTTP client requests.

``` javascript
> http.globalAgent
Agent 
{
  domain:
   Domain {
     domain: null,
     _events: { error: [Function] },
     _eventsCount: 1,
     _maxListeners: undefined,
     members: []
  },
  _events: { free: [Function] },
  _eventsCount: 1,
  _maxListeners: undefined,
  defaultPort: 80,
  protocol: 'http:',
  options: { path: null },
  requests: {},
  sockets: {},
  freeSockets: {},
  keepAliveMsecs: 1000,
  keepAlive: false,
  maxSockets: Infinity,
  maxFreeSockets: 256 
}
```
