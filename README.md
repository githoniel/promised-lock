# Promised-Lock

Promise化互斥锁， 申请锁后，只有锁释放才能使得下次申请锁能够Resolve

Promise mutex lock, after `requestLock`, other `requestLock` will block until other lock are released.

## API

- requestLock：Promise

申请锁，在锁全部执行完成的情况下，返回锁id

requestLock, if succeed, return lock id


- realseLock：Promise(id: Number)

释放指定id的锁

release lockid, let running `requestLock` to resolve

## Example

```js
const PromiseLock = require('promised-lock')

const lock = new PromiseLock()

const id = await lock.requestLock()
lock.release(id)

const id2 = await lock.requestLock()
await lock.requestLock() // should block until lock.release(id2)
```
