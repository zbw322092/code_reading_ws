# Receiver.js

1. `class Receiver` - `getInfo` method
The first two bytes in data framing contain `FIN`, `RSV1, RSV2, RSV3`, `Opcode`, `Mask` and `Payload length` info.<br/>

This method extra data from first two bytes from buffer and verifies whether these data are valid, if not, throw error. Otherwise sign these value to private value eg. `_fin`, `_opcode` and so on.

2. `readBuffer` is a key function in `class Receiver`
`readBuffer` reads specified data from buffer which is received from sender. We need these data to take further operation.

3. `startLoop` method
taking different action according to `_state`.

4. `getData` method
- read buffer according to `_payloadLength`.
- unmask data if necessary.
- process data according to `_opcode`.


5. `dataMessage` method and `controlMessage` method
`dataMessage` method
- process `data` according to `_opcode` and `_binaryType`.
- pass processed data into `onmessage` method.
- switch `_state` to `GET_INFO`.

Corresponding, `controlMessage` method processes control data frame.
It process data according to `_opcode` -- `onclose`, `onping` or `onpong`.

