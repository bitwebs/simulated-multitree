# Simulated MultiTree

I created this to work on some applications while Multitree finishes getting written. It probably won't be useful to most people.

```
npm i simulated-multitree
```

```js
import { SimulatedMultitree, SimulatedOplog, SimulatedRemoteOplog } from 'simulated-multitree'

// Create an multitree with a single writer
const db = new SimulatedMultitree()
db.addWriter(new SimulatedOplog())

// Create another multitree with its own writer
const db2 = new SimulatedMultitree()
db2.addWriter(new SimulatedOplog())

// Add them as writers to each other
db.addWriter(new SimulatedRemoteOplog(db2.writers[0]))
db2.addWriter(new SimulatedRemoteOplog(db.writers[0]))

// "Connect" them
db.writers[1].connect()
db2.writers[1].connect()

// "Disconnect" them
db.writers[1].disconnect()
db2.writers[1].disconnect()

// the rest of the API works like BitTree except there's also a `conflicts` array value on gets
```