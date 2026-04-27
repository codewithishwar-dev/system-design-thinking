# ⚠️ Concurrency Pitfall: Shared Integer Race Condition

> Even a simple shared integer can break everything.

---

## 🧠 The Scenario

Two threads operate on the same variable:

- Thread 1 → increments (`+1`)
- Thread 2 → decrements (`-1`)

### Expected Result
0
### Actual Result
❌ Unpredictable

---

## ❗ Why Does This Happen?

Because these operations are **NOT atomic**.

What looks like a single operation:
```java
value++;
```
Is actually broken into:

Read
Modify
Write

👉 Threads can interleave at any step → leading to inconsistent results.

🔁 Race Condition Visualization
Thread A: Read → Modify → Write
Thread B: Read → Modify → Write

⚠️ Interleaving causes unexpected outcomes
💥 The Problem
Data inconsistency
Unpredictable results
Hard-to-debug bugs

🌐 Java Example (Race Condition)

class Counter {
    int value = 0;

    void increment() {
        value++; // not atomic
    }

    void decrement() {
        value--; // not atomic
    }
}

public class Main {
    public static void main(String[] args) throws Exception {
        Counter counter = new Counter();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 10000; i++) counter.increment();
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 10000; i++) counter.decrement();
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println(counter.value); // ❌ unpredictable
    }
}

```
✅ Solutions (Java)
1. synchronized
Simple to implement
Ensures mutual exclusion
❌ Can block threads (performance cost)
synchronized void increment() {
    value++;
}
```


2. AtomicInteger
Lock-free thread-safe operations
Efficient for counters

```
import java.util.concurrent.atomic.AtomicInteger;

AtomicInteger counter = new AtomicInteger(0);
counter.incrementAndGet();

```
3. Locks (ReentrantLock)
More control over concurrency
Useful for complex scenarios
❌ More code complexity

🌐 JavaScript Example (Async Race Condition)

Even though JavaScript is single-threaded, async operations can still cause race conditions:
let counter = 0;

```
async function increment() {
  let temp = counter;   // read
  await Promise.resolve(); // simulate delay
  counter = temp + 1;   // write
}

async function decrement() {
  let temp = counter;   // read
  await Promise.resolve(); // simulate delay
  counter = temp - 1;   // write
}

async function run() {
  const tasks = [];

  for (let i = 0; i < 1000; i++) {
    tasks.push(increment());
    tasks.push(decrement());
  }

  await Promise.all(tasks);

  console.log(counter); // ❌ unpredictable
}

run();
```

🔐 JavaScript Fix (Mutex)

```
class Mutex {
  constructor() {
    this.locked = false;
    this.queue = [];
  }

  lock() {
    return new Promise(resolve => {
      if (!this.locked) {
        this.locked = true;
        resolve();
      } else {
        this.queue.push(resolve);
      }
    });
  }

  unlock() {
    if (this.queue.length > 0) {
      const next = this.queue.shift();
      next();
    } else {
      this.locked = false;
    }
  }
}

const mutex = new Mutex();
let safeCounter = 0;

async function safeIncrement() {
  await mutex.lock();
  safeCounter++;
  mutex.unlock();
}

async function safeDecrement() {
  await mutex.lock();
  safeCounter--;
  mutex.unlock();
}
}
```
🎯 Key Takeaway

Concurrency bugs don’t fail loudly.
They fail silently.

And that’s what makes them dangerous.

🚀 Learning Note

This changed how I think about multi-threading and shared state.

🏷️ Tags

concurrency multithreading race-condition java javascript backend
📌 Author

#CodeWithIshwar | Ishwar Chandra Tiwari

---

## 💡 Quick next step (do this)
- Add your **image** (`/assets/concurrency.png`)
- Add this line at top:

```markdown
![Concurrency Diagram](assets/concurrency.png)


