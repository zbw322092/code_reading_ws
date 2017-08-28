# Sender.js
1. JS `static`
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static

The static keyword defines a **static method** for a **class**.

Static method calls are made directly on the class and are **not callable on instances of the class**. Static methods are often used to create utility functions.

2. Node.js `Buffer` Module
- Instances of the `Buffer` class are similar to arrays of integers but correspond to **fixed-sized, raw memory allocations outside the V8 heap**. The size of the Buffer is established when it is created and **cannot be resized**.

- `Buffer.from(), Buffer.alloc(), and Buffer.allocUnsafe()`
https://nodejs.org/api/buffer.html#buffer_buffer_from_buffer_alloc_and_buffer_allocunsafe

Starting in Node.js 8.0.0, Buffer(num) and new Buffer(num) will return a Buffer with initialized memory.<br/>

To make the creation of Buffer instances **more reliable and less error prone**, the various forms of the `new Buffer()` constructor have been **deprecated** and replaced by separate `Buffer.from()`, `Buffer.alloc()`, and `Buffer.allocUnsafe()` methods.

- `Class Method: Buffer.allocUnsafe(size)`
https://nodejs.org/api/buffer.html#buffer_class_method_buffer_allocunsafe_size
Allocates a new Buffer of size bytes.
The underlying memory for Buffer instances created in this way is **not initialized**.

- `buf.writeUInt16BE(value, offset[, noAssert])`
https://nodejs.org/api/buffer.html#buffer_buf_writeuint16be_value_offset_noassert
value should be a valid `unsigned 16-bit integer`.

- `buf.writeUInt32BE(value, offset[, noAssert])`
https://nodejs.org/api/buffer.html#buffer_buf_writeuint32be_value_offset_noassert

value should be a valid `unsigned 32-bit integer`.

- `buf.copy(target[, targetStart[, sourceStart[, sourceEnd]]])`
https://nodejs.org/api/buffer.html#buffer_buf_copy_target_targetstart_sourcestart_sourceend
Copies data from a region of buf to a region in target even if the target memory region overlaps with buf.

- `Class Method: Buffer.byteLength(string[, encoding])`
https://nodejs.org/api/buffer.html#buffer_class_method_buffer_bytelength_string_encoding

- `buf.write(string[, offset[, length]][, encoding])`


3. `static frame` method
This method in `Sender` class take responsibility for constructing a websocket `data framing`.
> RFC 6455 - 5.2.  Base Framing Protocol

4. Node.js `crypto` module
- `crypto.randomBytes(size[, callback])`
https://nodejs.org/api/crypto.html#crypto_crypto_randombytes_size_callback

Generates cryptographically strong pseudo-random data. The size argument is a number indicating the number of **bytes** to generate.

5. `close` method
...If there is a body, the first two bytes of the body MUST be a **2-byte unsigned integer** (in network byte order) representing **a status code** with value /code/ defined in Section 7.4.

6. `doClose` method
Sending a websoket closing data framing which is defined by `Sender.frame` method.

7. `ArrayBuffer`
The `ArrayBuffer` object is used to represent **a generic, fixed-length raw binary data buffer**. You cannot directly manipulate the contents of an `ArrayBuffer`; instead, you create one of the `typed array objects` or a `DataView` object which represents the buffer in a specific format, and use that to read and write the contents of the buffer.

- ArrayBuffer.isView(arg)
Returns `true` if arg **is one of the ArrayBuffer views**, such as `typed array objects` or a `DataView`. Returns false otherwise.


8. `DataView`
The DataView view provides a low-level interface for reading and writing multiple number types in an ArrayBuffer irrespective of the platform's endianness.


9. **`frame`** and **`sendFrame`** are two key functions in `Sender` constructor.

10. `Array.prototype.shift()` and `Array.prototype.unshift()`
- `Array.prototype.shift()` The shift() method removes the first element from an array and returns that element. This method changes the length of the array.
- `Array.prototype.unshift()` The unshift() method adds one or more elements to the beginning of an array and returns the new length of the array.


