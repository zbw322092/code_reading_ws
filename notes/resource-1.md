# Websockets 101
http://lucumr.pocoo.org/2012/9/24/websockets-101/

## handshake
- It upgrades your connection from HTTP to something else. For the internal protocol we recommend to customers we upgrade our HTTP connection basically to a raw TCP connection. Websockets are not an upgrade to TCP, it's an upgrade to a message based communication.
- Websockets upgrade from HTTP because it was believed that people would develop servers that serve **both websocket connections as well as HTTP ones**. 
- the advantage is that websockets use **the same ports** as HTTP and HTTPS do and that is a huge win. It's a win because these are privileged ports (< 1024) and they are traditionally handled differently than non privileged ports. 


## Framing
- websocket is not a stream based protocol like TCP, it's `message based`.
- ...Websockets makes this easier because it **puts a frame around everything**.
- payload_len (7 bits): the length of the payload. 7 bits is not enough? Of course not. Websocket frames come in the following length brackets:<br/>
`0-125` mean the payload is that long. <br/>
`126` means that the **following two bytes** indicate the length.<br/>
`127` means the **next 8 bytes** indicate the length. So it comes in **~7bit, 16bit and 64bit**. 

## Fragmentation and Masking
- The logic for joining frames is roughly this: receive first frame, remember `opcode`, concatenate frame payload together until the `fin` bit is set. Assert that the `opcode` for each package is zero.

### Heartbeating
- With websockets you can send the `ping opcode` at any time to ask the other side to `pong`. `Pings` can be sent whenever an endpoint thinks it should and a `pong` is sent “as soon as is practical”.



