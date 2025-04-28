# Concurrency

## What is concurrency?

Concurrency is the ability of a program to execute multiple tasks simultaneously. It allows for better resource utilization and can improve the performance of applications, especially those that are I/O-bound or require parallel processing.

There are mainly three types of concurrency in Python:

1. **Threading**: Using threads to run multiple tasks concurrently within a single process. Suitable for I/O-bound tasks.
2. **Multiprocessing**: Using multiple processes to run tasks concurrently. Suitable for CPU-bound tasks.
3. **Asyncio**: Using asynchronous programming to run tasks concurrently. Suitable for I/O-bound tasks.

## Threading

basic threading example:

```python
import threading
import time
from concurrent.futures import ThreadPoolExecutor

def threaded_function():
    for number in range(3):
        print(f"Printing from {threading.current_thread().name}. {number=}")
        time.sleep(0.1)

with ThreadPoolExecutor(max_workers=4, thread_name_prefix="Worker") as executor:
    for _ in range(4):
        executor.submit(threaded_function)

# Output:
# Printing from Worker_0. number=0
# Printing from Worker_1. number=0
# Printing from Worker_2. number=0
# Printing from Worker_3. number=0
# Printing from Worker_0. number=1
# Printing from Worker_2. number=1
# Printing from Worker_1. number=1
# Printing from Worker_3. number=1
# Printing from Worker_0. number=2
# Printing from Worker_2. number=2
# Printing from Worker_1. number=2
# Printing from Worker_3. number=2
```

Thread safety issues occur because of two factors:

- **Shared state**: When multiple threads access and modify the same data simultaneously, it can lead to race conditions, causing inconsistent or unpredictable results.
- **Non-atomic operations**: Operations that aren’t atomic (indivisible) can be interrupted midway by other threads, resulting in partial updates or corrupted data.

## Using `threading.Lock` for mutual exclusion

```python
import threading
import time
from concurrent.futures import ThreadPoolExecutor

class BankAccount:
    def __init__(self, balance=0):
        self.balance = balance
        self.account_lock = threading.Lock()

    def withdraw(self, amount):
        with self.account_lock:
            if self.balance >= amount:
                new_balance = self.balance - amount
                print(f"Withdrawing {amount}...")
                time.sleep(0.1)  # Simulate a delay
                self.balance = new_balance
            else:
                raise ValueError("Insufficient balance")

    def deposit(self, amount):
        with self.account_lock:
            new_balance = self.balance + amount
            print(f"Depositing {amount}...")
            time.sleep(0.1)  # Simulate a delay
            self.balance = new_balance

account = BankAccount(1000)

with ThreadPoolExecutor(max_workers=3) as executor:
    executor.submit(account.withdraw, 700)
    executor.submit(account.deposit, 1000)
    executor.submit(account.withdraw, 300)

print(f"Final account balance: {account.balance}")

# Output:
Withdrawing 700...
Depositing 1000...
Withdrawing 300...
Final account balance: 1000
```

## `threading.RLock` for Reentrant Locking

Reentrant locks (`threading.RLock`) allow a thread to acquire the same lock multiple times without causing a deadlock. This is useful when a thread needs to call a function that requires the same lock it already holds.

Key points:
- **Reentrant**: A thread can acquire the lock multiple times without blocking itself.
- **Release**: Lock if fully released the same number of times it was acquired.

```python
import threading

rlock = threading.RLock()

def inner_task():
    with rlock:
        print("Inner task acquired lock.")

def outer_task():
    with rlock:
        print("Outer task acquired lock.")
        inner_task()

thread = threading.Thread(target=outer_task)
thread.start()
thread.join()
```

## Limiting Access With `Semaphore`

`Semaphore` is a synchronization primitive that allows a limited number of threads to access a shared resource concurrently. It's especially useful in secnarios like:

- Limiting the number of connections to a server
- Controlling access to limited resources (e.g., database connections, file handles)

Key points:

- Initialized with a positive integer, representing available permits.
- `.acquire()` decrements the semaphore count; threads wait if the count is zero.
- `.release()` increments the semaphore count, signaling that a permit is available.

```python
import threading
import time

semaphore = threading.Semaphore(2)  # max 2 threads simultaneously

def worker(worker_id):
    print(f"Worker {worker_id} waiting...")
    with semaphore:
        print(f"Worker {worker_id} working...")
        time.sleep(2)
        print(f"Worker {worker_id} done.")

threads = [threading.Thread(target=worker, args=(i,)) for i in range(4)]

for t in threads:
    t.start()
for t in threads:
    t.join()

# Output:
# Worker 0 waiting...
# Worker 0 working...
# Worker 1 waiting...
# Worker 1 working...
# Worker 2 waiting...
# Worker 3 waiting...
# Worker 0 done.
# Worker 2 working...
# Worker 1 done.
# Worker 3 working...
# Worker 2 done.
# Worker 3 done.
```

## Using Synchronization Primitives for communication and coordination

### Events for Signaling

```python
import threading
import time

event = threading.Event()

def waiter():
    print("Waiter thread is waiting for event...")
    event.wait()
    print("Waiter thread received event!")

def notifier():
    print("Notifier thread sleeping...")
    time.sleep(2)
    event.set()
    print("Notifier thread set event.")

t1 = threading.Thread(target=waiter)
t2 = threading.Thread(target=notifier)

t1.start()
t2.start()

t1.join()
t2.join()

# Output:
# Waiter thread is waiting for event...
# Notifier thread sleeping...
# Notifier thread set event.
# Waiter thread received event!
```

### Conditions for Conditional Waiting

A `Condition` (`threading.Condition`) enables threads to pause execution and wait until cetain conditions are met.
It's ideal for producer-consumer scenarios, where one or more threads produce data and others consume it.

Key points:

- Threads call `.wait()` to block until notified.
- Use `.notify()` or `.notify_all()` to wake up waiting threads (`notify()` for one thread, `notify_all()` for all).

```python
import threading
import time

condition = threading.Condition()
queue = []

def consumer():
    with condition:
        print("Consumer waiting for item...")
        while not queue:
            condition.wait()
        item = queue.pop(0)
        print(f"Consumer got item: {item}")

def producer():
    with condition:
        print("Producer creating item...")
        queue.append("data")
        condition.notify()

c = threading.Thread(target=consumer)
p = threading.Thread(target=producer)

c.start()
time.sleep(1)  # ensure consumer waits first
p.start()

c.join()
p.join()

# Output:
# Consumer waiting for item...
# Producer creating item...
# Consumer got item: data
```

### Barriers for Coordination

```python
Barrier(parties, action=None, timeout=None)
```

```python
import threading
import time

# Barrier for synchronizing exactly 3 threads
barrier = threading.Barrier(3)

def worker(worker_id):
    print(f"Worker {worker_id}: preparing")
    time.sleep(worker_id)  # simulate varying preparation times
    print(f"Worker {worker_id}: ready and waiting at barrier")

    barrier.wait()  # threads pause here until all 3 have called wait()

    print(f"Worker {worker_id}: passed the barrier, continuing")

# Create exactly 3 threads
threads = [
    threading.Thread(target=worker, args=(i,))
    for i in range(3)
]

for t in threads:
    t.start()

for t in threads:
    t.join()

print("All threads have passed the barrier.")

# Output:
# Worker 0: preparing
# Worker 1: preparing
# Worker 2: preparing
# Worker 0: ready and waiting at barrier
# Worker 1: ready and waiting at barrier
# Worker 2: ready and waiting at barrier
# Worker 2: passed the barrier, continuing
# Worker 0: passed the barrier, continuing
# Worker 1: passed the barrier, continuing
# All threads have passed the barrier.
```

| Primitive | Use-case                   | Key operations                       |
| --------- | -------------------------- | ------------------------------------ |
| RLock     | Reentrant locking          | `acquire()`, `release()`             |
| Semaphore | Limit concurrent access    | `acquire()`, `release()`             |
| Event     | Signaling between threads  | `set()`, `clear()`, `wait()`         |
| Condition | Conditional waiting        | `wait()`, `notify()`, `notify_all()` |
| Barrier   | Coordination among threads | `wait()`                             |

## Summary

- Identify race conditions in code
- Use `Lock` and `RLock` to protect shared resources
- Use `Semaphore` to limit concurrent access to resources
- Leverage `Event` for signaling between threads
- Use `Condition` for complex thread communication
- Use `Barrier` for coordinating multiple threads
