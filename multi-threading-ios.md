### Queues
- Multithreading is mostly about "queue" in iOS.
- Functions (usually closures) are simply lined up in a queue.
- Then those functions are pulled off the queue and executed on an associated thread(s).
- Queues can be "serial" (one closure a time) or "concurrent".
- GCD (Grand Central Dispatch), you can do locking, protect, critical sections readers and writers synchronous dispatch etc
- OperationQueue, Operation

### Main Queue
UI runs on a single serial queue called the "main queue."
All UI activity **MUST** occur on this queue and this queue only.

And, conversely, non-UI activity that is at all time consuming must NOT occur on that queue.

Functions are pulled off and worked on the main queue only with it is "quiet".

### Global Queues
dFor non-main-queue work, you are usually going to use a shared, global, concurrent queue.

Getting a Queue
`let mainQueue = DispatchQueue.main`

Getting a global, shared, concurrent "background queue"
This is almost always what you will use to get activity off the main queue.

`let backgoundQueue = DispatchQueue.global(qos: DispatchQoS)`
QoS = qulity of service
- `DispatchQoS.userInteractive // high priority, only do something short and quick`
- `DispatchQoS.userInitiated // high, but might take a little bit of time`
- `DispatchQoS.background // not directly inited by user, so can run as slow as needed`
- `DispatchQoS.utility // long-running bg process, low priority`

### Putting a block of code on the Queue
`queue.async { ... }`
`queue.sync { ... }`


### Getting a non-global Queue
very rarely you might need a queue other than main or Global
your own serial queue (use this only if you have multiple, serially dependent activities)
`let serialQueue = DispatchQueue(label: "MySerialQ")`

concurrent:
`let concurrentQueue = DispatchQueue(label: "MyConcorrentQ", attributes: .concurrent)`




### example of URLSession

```
let session = URLSession(configuration: .default)
if let url = URL(string: "http://...") {
    let task = session.dataTask(with: url) { (data: Data?, response, error) in
        DispatchQueue.main.async {
            // do UI stuff
        }
    }
    task.resume()
}
```
