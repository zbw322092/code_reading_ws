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


3. `static frame` method
This method in `Sender` class take responsibility for constructing a websocket `data framing`.
> RFC 6455 - 5.2.  Base Framing Protocol

