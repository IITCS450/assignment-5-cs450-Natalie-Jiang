# Assignment 5

## Context Switching approach
The code uses user-level context switching to manage multiple threads within a process. Each thread has its own stack and a saved register context (edi, esi, ebx, ebp, and eip). This represents the thread's execution state. When thread_yield() is called, the current thread's context is saved, and a round-robin scheduler selects the next runnable thread. The uswtch restores the next thread's context. This allows execution to resume from its saved instruction pointer. New threads are initialized so that they begin execution in thread_stub(). This calls the thread function and marks the thread as a zombie when it is completed. Then, it yields to allow other threads to run.

## Limitations
There are multiple limitations. It only supports a fixed number of threads. For this, it was 8 threads. Each thread is assigned a fixed 4 KB stack. This limits the amount of work each thread can safely perform. The scheduling is cooperative. This means that the threads must explicitly call thread_yield(). If they don't call thread_yield(), it will block the others. The mutex implementation uses busy-waiting with waiting. This can be inefficient. Also, the scheduler uses a simple round-robin with no priorities, and all threads share the same address space. This requires careful synchronization to avoid data corruption.
