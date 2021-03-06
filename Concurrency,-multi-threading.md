This document describes various concurrency, multi-threading, parallel programming methods and concepts. The purpose is to write a single document/wiki that contains everything you need to know about concurrency. Things should be explained clearly yet in as great detail as possible. You are welcome to contribute to this document.

If you are interested in contributing to this document, you can ask me to add you as a contributor or you can just fork this.

Note 1: This document mainly discusses modern OS and hardware.

Note 2: While attention is paid to what is written here, there is no guarantee that this document is correct at its entirety.

Table of Contents
Approaches to concurrency

Processes
Threads
Green Threads
Green Processes
Isolates
Synchronization primitives

Locks
Mutex
Semaphores
Monitors
Message Passing
Higher-Level Frameworks and Languages

Microsoft's TPL and other asynchronous features
Apple's GCD and blocks
Clojure
Erlang
Node.js
Python gevent
HTML5 Web Workers

Processes

Processes are operating system (OS) managed and in case of a modern OS they are truly concurrent in the presence of suitable hardware support (multiprocessor and multicore systems).

Processes are scheduled by the operating system's [scheduler](http://en.wikipedia.org/wiki/Scheduling_(computing\)). They may be made up of multiple [threads of execution](http://en.wikipedia.org/wiki/Thread_(computer_science\)) that execute instructions concurrently.

Processes exist within their own address space. No other process can read or write to another one's memory, because the OS secures this with process isolation as the OS is the one who manages the processes.

Processes are heavy and spawning many of them (in contrast to other concurrency models) is not recommended. Creating a process requires creating an entirely new virtual address space.

Context switching between processes requires a lot of work. This means saving of the entire CPU state (all processor registers that were in use, program counter, etc.) into PCB (usually). Context switching also involves switching the MMU context and keeping OS related data.

Processes can't talk to each other directly (in modern OS). Instead the OS provides facilities for inter-process communication.

Typical ways of inter-process communication involve files, [signals](http://en.wikipedia.org/wiki/Signal_(computing\)), sockets, message queues, (named) [pipes](http://en.wikipedia.org/wiki/Pipeline_(Unix\)), [semaphores](http://en.wikipedia.org/wiki/Semaphore_(programming\)), shared memory and even memory-mapped files.

Processes are all about preemptive multitasking (today) meaning that the OS decides when a process is preempted ("goes to sleep") and which process goes "alive" next.


Threads

Threads, like processes, are also OS managed. Threads share the same address space of their parent process. This means that processes can spawn threads indirectly using OS provided functionality (e.g. CreateThread or pthread_create).

On a single processor, multithreading generally occurs by time-division multiplexing (as in multitasking): the processor switches between different threads. This context switching generally happens frequently enough that the user perceives the threads or tasks as running at the same time. On a multiprocessor (including multi-core system), the threads or tasks will actually run at the same time, with each processor or core running a particular thread or task.

Many modern operating systems directly support both [time-sliced](http://en.wikipedia.org/wiki/Preemption_(computing\)#Time_slice) and multiprocessor threading with a [process scheduler](http://en.wikipedia.org/wiki/Scheduling_(computing\)).

Like processes, threads are about preemptive multitasking and the OS decides when they are preempted. To avoid preemption with threads, mutex can be used. Windows also offers support for Critical Sections with two functions EnterCriticalSection and LeaveCriticalSection.

Communication between threads is far simpler than inter-process communication between processes. This is mainly due to the shared memory, but also due to the fact that the strict security constraints the OS puts on processes do not exist with threads.

Memory usage

Threads are generally said to be "lightweight", but that is relative. Threads have to support the execution of native code so the OS has to provide a decent-sized stack, usually measured in megabytes. In Windows, the [default stack reservation size](http://msdn.microsoft.com/en-us/library/windows/desktop/ms686774(v=vs.85\).aspx) used by the linker is 1 MB. In Linux, the typical thread stack size is between 2 MB and 10 MB. This means that in Linux, creating 1000 threads would equal to memory usage from ~2 GB to ~10 GB, without even beginning to do any actual work with the threads.

Determining stack size on Linux

You can rather easily determine the default stack size for Linux OS by running the following:

$ ulimit -a | grep stack
stack size    (kbytes, -s) 8192
The above output was from Ubuntu 11 x86. We can also test this with some code:

void makeTenThreads()
{
    std::vector<pthread_t> threads;

    for (int i = 0; i < 10; i++)
    {
        threads.push_back(pthread_t(0));
        pthread_create(&threads.back(), 0, &doNothing2, 0);
    }

    std::vector<pthread_t>::iterator itr = threads.begin();
    while (itr != threads.end())
    {
        pthread_join(*itr, 0);
        ++itr;
    }

    sleep(11);

    threads.clear();
}

int main()
{
    makeTenThreads();
    sleep(10);
}
Running pmap -x 1234 where 1234 is the PID will give us 10 x 8192K blocks allocated, because we created 10 threads and each of them got 8 MB allocated.

Setting the stack size

Thread default stack size varies depending on the OS and you can actually set it on your own. On Linux, you call pthread_attr_setstacksize and on Windows it can be specified as a parameter to CreateThread.

The number of threads a process can create is limited by the available virtual memory and depends on the default stack size. On Windows, if every thread has 1 MB of stack space, you can create a maximum of 32 threads. If you reduce the default stack size, you can create more threads. These details vary greatly depending on the platform and libraries.

Reducing the thread stack size will not reduce overhead in terms of CPU or performance. Your only limit in this respect is the total available virtual address space given to threads on your platform. Generally you should not change the stack size, because you can't really compute how much you need for an arbitrary thread, as it totally depends on the code run. You would have to analyze the entire code and the resulting disassembly executed by the thread to know how much stack size to use. This is non-trivial.

"Threads are lightweight"

Threads are "lightweight processes", not "lightweight" themselves as some may claim. They require less resources to create and to do context switching as opposed to processes, but it still is not cheap to have many of them running at the same time.

While thread context switching still involves restoring of the program counter, CPU registers, and other potential OS data, they do not need the context switch of an MMU unlike processes do, because threads share the same memory. Context switching with threads is less of a problem unless you have many threads.

Race conditions

Since memory/data is shared among threads in the same process, applications frequently need to deal with race conditions. [Thread Synchronization](http://en.wikipedia.org/wiki/Synchronization_(computer_science\)#Thread_or_process_synchronization) is needed. Typical synchronization mechanisms include Locks, Mutex, Monitors and Semaphores. These are concurrency constructs used to ensure two threads won't access the same shared data at the same time, thus achieving correctness.

Programming with threads involve hazardous race conditions, deadlocks and livelocks. This is often said to be one of the bad things about threads along with the overhead they bring.

Summary

Threads are good for concurrent CPU heavy work across 1-n processors and cores within a single application/process. This is, because they scale to cores and CPUs thanks to the OS scheduler. For IO heavy work, threads are a nightmare, because that usually involves spawning of multiple threads for shorter periods of time.

When to use

You need plenty of CPU.
You keep the threads running for a longer time.
You do not spawn and kill and spawn and kill threads too often.
You do not need many threads.
An example of a good use for a thread could be a game. Running e.g. AI logic on a separate thread makes sense, because the thread is spawned once and kept alive for a long time. AI logic also requires plenty of CPU making threads very good for such purposes.

Short-lived, frequently spawned threads make little sense. Building a chat web application that involves 1000 concurrent active chatters are an example when not to use threads. Memory usage would be high, context switching would take too much time relative to the actual application. Creating threads and killing them that often has an unacceptable high overhead. A chat requires more IO than CPU work, thus, threads do not suit that situation.


Green Threads

Green threads are threads that are scheduled by a virtual machine (VM). In contrast, typical threads are scheduled by the underlying operating system. Green threads emulate multithreaded environments without relying on any native OS capabilities, and they are managed in user space instead of kernel space, enabling them to work in environments that do not have native thread support.

Native threads can switch between threads pre-emptively, switching control from a running thread to a non-running thread at any time. Green threads only switch when control is explicitly given up by a thread (Thread.yield(), Object.wait(), etc.) or a thread performs a blocking operation (read(), etc.). Whether a blocking call causes yielding depends on the virtual machine implementation.

On multi-CPU machines, native threads can run more than one thread simultaneously by assigning different threads to different CPUs. Green threads run on only one CPU, because every green thread runs on the same operating system thread. This means that a green thread that blocks will block every other green thread as well.

Green threads can be started much faster on some VMs. They significantly outperform Linux native threads on thread activation and synchronization. Native threads have better performance on I/O and context switching operations, however.

Green threads are a good choice over native threads if the platform does not provide support for threading. Another reason is that if your code is not thread-safe or if you need to spawn many threads and often since this is cheaper with green threads.

The Erlang virtual machine has what might be called 'green processes' - they are like operating system processes (they do not share state like threads do) but are implemented within the Erlang Run Time System (erts). These are sometimes erroneously cited as green threads.

Summary

Green threads are rarely used nowadays. They provide little use and have their drawbacks.

When to use

The underlying platform does not provide support for threads.
We need to spawn many threads or often.
Our code is not thread-safe.

Green Processes

Green processes are like operating system processes except that they are implemented in a virtual machine on the user space. This means that green processes do not share state like threads do, freeing us from the race condition hazards that threads pose.

The Erlang Run Time System (erts) implements green processes. These are sometimes erroneously cited as green threads.

Green processes are neither operating system processes nor threads, but lightweight processes. It has been estimated that Erlang's green processes take around 300 WORDs to create, thus many of them can be created without degrading the performance. It has also been proven to be possible to create even 20 million processes. These figures are highly implementation dependent, but they show the potential of green processes.

One reason why green processes can be so lightweight as opposed to operating system processes is that green processes totally lack of any type of security restrictions or other unnecessary overhead that the OS has to put on its processes. Another reason for their lightness is that the virtual machine is fully aware of the application that uses these processes, unlike in case of an OS that has less of an idea of what an application might do.

Inter-process communication works via shared-nothing asynchronous message passing style. The use of message passing eliminates hazards such as deadlocks and livelocks that threads have and allow for clean communication.


Isolates

Isolates are a concurrency mechanism used in Google Dart. Isolates are spawned and use message passing. They are inspired by Erlang's green processes.

There are two types of isolates, heavy and light. These two differ dramatically, and the programmer has to know which one to use in which scenario. Luckily isolates offer an intuitive API that works the same way for both light and heavy isolates so it is easy to change the type of an isolate at any time.

Isolates are independent of each other. This means they do not share state as one might guess from the use of message passing.

Heavy isolates

Heavy isolates use threads behind the scenes. Typical synchronization mechanisms such as locks and monitors are not needed nor do they exist in the programmers eyes. Heavy isolates use message passing and internally rely on operating system threads. It's up to the implementation to decide what kind of synchronization mechanism to use (e.g. monitors) and that mechanism may even vary depending on scenarios.

Due to use of message passing you are free from thread related problems such as deadlocks and spinlocks. Heavy isolates are essentially a nice implementation on top of native threads.

Light isolates

Light isolates are different from heavy isolates in the sense that the underlying implementation does not use threads. Light isolates are single-threaded, they live on the thread that spawned the light isolate. For example, one may spawn two heavy isolates which both spawn a light isolate and in this case, you would have two native threads both running one light isolate.

Light isolates are very efficient in context switching and to create/kill. And in fact, it is very well possible to create millions of light isolates. This allows for concurrent, real-time, web applications for instance.

Beware that blocking in a light isolate blocks the rest of the isolates on that thread.

Heavy vs light isolates

Heavy isolates come with some of the benefits and drawbacks of threads. The same applies to light isolates, they come with the problems and benefits of single-threaded evented systems.

When to use heavy isolates

You need CPU heavy work.
You do not need multiple isolates.
You are not spawning and killing isolates too often.
When to use light isolates

You are IO bound rather than CPU bound.
You need several isolates or you spawn/kill them frequently.
If you were to program a game, you should use heavy isolates for the AI. If you were programming a web server, you would use light isolates for handling requests.

There is no reason not to use both and in fact, using both at times makes sense.

Communication

As said earlier, isolates rely on message passing. There is no shared data and communication is done through ports. This communication allows you to also restart parts of the program if something goes wrong and an isolate lives as long as its port(s) are open. The message passing is asynchronous.

Here's an example code sample written in Dart:

class Worker extends Isolate {
    Worker() : super.heavy();

    main() {
        this.port.receive(
            void _(var message, SendPort replyTo) {
                print("Message received: ${message}");
                replyTo.send("sup");
                this.port.close();
            }
        );
    }
}
The Worker class extends the Isolate class, and when it's instantiated, it calls the Isolate class' heavy constructor which means that this Worker class uses a heavy isolate.

We are supplying an anonymous callback function to the receive-method. The function receives message and replyTo arguments. Since the message is specified as var, the sender can send anything from integers to strings to complex objects. The same API works with light isolates as well.

Other benefits of isolates

Isolates have their own heap. This means that garbage collection can happen per isolate. This solves the big problem of today's garbage collectors which need to pause the entire program to clean the garbage. With isolates, only one isolate needs to be paused while being cleaned allowing the rest of the program to continue. This has huge benefits for UI-centric software where a garbage collector pause would freeze the UI.

It is also a possibility to send messages between isolates on different hosts (called remote isolates), although Dart does not implement this yet.

Isolates may also be used to enforce security rules on ports and to even replace the Same Origin Policy.


Locks

[Locks](http://en.wikipedia.org/wiki/Lock_(computer_science\)) are usually advisory locks, where each thread cooperates by acquiring the lock before accessing the corresponding data. Most locking designs block the execution of the thread requesting the lock until it is allowed to access the locked resource. A spinlock is a lock where the thread simply waits ("spins") until the lock becomes available. It is very efficient if threads are only likely to be blocked for a short period of time, as it avoids the overhead of operating system process re-scheduling. It is wasteful if the lock is held for a long period of time. Careless use of locks can result in deadlock or livelock. In many programming languages Locks are the easiest synchronization mechanism to use.


Mutex

A mutex is similar to a monitor; it prevents the simultaneous execution of a block of code by more than one thread at a time. In fact, the name "mutex" is a shortened form of the term "mutually exclusive." Unlike monitors, however, a mutex can be used to synchronize threads across processes. When used for inter-process synchronization, a mutex is called a named mutex because it is to be used in another application, and therefore it cannot be shared by means of a global or static variable. It must be given a name so that both applications can access the same mutex object. Mutexes unlike Locks or Monitors, can be used for inter-process synchronization.


Semaphores

[Semaphores](http://en.wikipedia.org/wiki/Semaphore_(programming\)) is a variable or an abstract data type that provides a simple, but useful abstraction for controlling access by multiple processes to a common resource in a parallel programming environment. Thus, Semaphores are not used for intra-process synchronization, but only inter-process synchronization. A Semaphore is essentially a record of how many units of a particular resource are available, coupled with operations to safely (i.e. without race conditions) adjust that record as units are required or become free, and if necessary wait until a unit of the resource becomes available.

Semaphores which allow an arbitrary resource count are called counting semaphores, while semaphores which are restricted to the values 0 and 1 (or locked/unlocked, unavailable/available) are called binary semaphores. A mutex is essentially the same thing as a binary semaphore, and sometimes uses the same basic implementation. However, the term "mutex" is used to describe a construct which prevents two processes from executing the same piece of code, or accessing the same data, at the same time. The term "binary semaphore" is used to describe a construct which limits access to a single resource on the system.


Monitors

[Monitors](http://en.wikipedia.org/wiki/Monitor_(synchronization\)) prevent blocks of code from simultaneous execution by multiple threads just like Locks. In fact, Locks are sometimes based on Monitors, like in case of C#. Monitors provide a mechanism for threads to temporarily give up exclusive access, in order to wait for some condition to be met, before regaining exclusive access and resuming their task.


Message Passing

Message passing is a form of communication used in parallel computing, object-oriented programming, and interprocess communication. In this model, processes or objects can send and receive messages -- consisting of zero or more bytes, complex data structures, or even segments of code -- to other processes. By waiting for messages, processes can also synchronize.

Message passing has several forms and may be implemented differently:

Communication can be either synchronous or asynchronous.
Messages may be passed one-to-one (unicast), one-to-many (multicast or broadcast), many-to-one (client-server) or even many-to-many (AllToAll).
Messages may or may not be received in the original order they were sent.
Messages may or may not be sent reliably.
Implementations of concurrent systems that use message passing can either have message passing as an integral part of the language, or as a series of library calls from the language. Message passing systems have been called "shared nothing" systems because the message passing abstraction hides underlying state changes that may be used in the implementation of sending messages.

Messages are also commonly used in the same sense as a means of inter-process communication; the other common technique being streams or pipes, in which data are sent as a sequence of elementary data items instead.

Synchronous vs asynchronous message passing

Synchronous message passing systems require the sender and receiver to wait for each other to transfer the message. That is, the sender will not continue until the receiver has received the message.

Synchronous communication has two advantages. The first advantage is that reasoning about the program can be simplified in that there is a synchronisation point between sender and receiver on message transfer. The second advantage is that no buffering is required. The message can always be stored on the receiving side, because the sender will not continue until the receiver is ready.

Asynchronous message passing systems deliver a message from sender to receiver, without waiting for the receiver to be ready. The advantage of asynchronous communication is that the sender and receiver can overlap their computation because they do not wait for each other.

Synchronous communication can be built on top of asynchronous communication by ensuring that the sender always wait for an acknowledgement message from the receiver before continuing. The buffer required in asynchronous communication can cause problems when it is full. A decision has to be made whether to block the sender or whether to discard future messages. If the sender is blocked, it may lead to an unexpected deadlock. If messages are dropped, then communication is no longer reliable.


