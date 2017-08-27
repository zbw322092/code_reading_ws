# Websockets 101
http://lucumr.pocoo.org/2012/9/24/websockets-101/

## Framing
- websocket is not a stream based protocol like TCP, it's `message based`.
- ...Websockets makes this easier because it **puts a frame around everything**.
- payload_len (7 bits): the length of the payload. 7 bits is not enough? Of course not. Websocket frames come in the following length brackets:<br/>
`0-125` mean the payload is that long. <br/>
`126` means that the **following two bytes** indicate the length.<br/>
`127` means the **next 8 bytes** indicate the length. So it comes in **~7bit, 16bit and 64bit**. 

