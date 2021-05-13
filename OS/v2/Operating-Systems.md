# Operating Systems Notes

## Introduction

### Types of OS

#### Simple batch System

- no direct interaction between user and the computer
- user has to submit a job(written on cards or tape) to a computer operator
- jobs are batched together by type of languages and requirement

#### Multiprogramming Batch System

- the operating system picks up and begins to execute one of the jobs from memory.
- once this job needs an I/O operation, OS switches to another job
- jobs in the memory are always less than the number of jobs on disk(Job Pool).
- if several jobs are ready to run at the same time, then the system chooses which one to run through the process of CPU Scheduling.
- CPU will never be idle
- **Time Sharing System** are an extension of multiprogramming systems

#### Multiprocessor System

- consists of several processors that share a common physical memory.
- all processors operate under single operating system.
- Multiplicity of the processors and how they do act together are transparent to the others.
-

#### Desktop System

#### Distributed Operating System

- The motivation behind developing distributed operating systems is the availability of powerful and inexpensive microprocessors and advances in communication technology.
- advancement in technology have made it possible to design and develop distributed systems comprising of many computers that are inter connected by communication networks.
- main benefit is its low price/performance ratio

##### Client-Server Systems

- is a computing model in which the server hosts, delivers and manages most of the resources and services to be consumed by the client.
- has one or more client connected to a central server over a network or internet connection.
- also known as a networking computing model or client/server network
-

#### Clustered System

#### Realtime Operating System

#### Handheld OS

## Structures

### Services

#### User Interfaces

allows user to interact with the system services via system calls

- Command-line
- GUI
- Batch (older system using punchcards)

#### Other System Services that are helpful to user

- Program Execution
- I/O Operations
- File-system Manipulation
- Communications
- Error Detection

#### Services that ensure efficient OS Operation

- **resource allocation**
  - CPU cycles
  - main memory
  - storage space
  - peripheral devices
- **accounting**
  - keeping track of system activity and resource usage, for billing or statistic usage.
- **protection and security**

### System Calls

- provide a means for user or application programs to call upon the services of the operating system.
- a system call is the programmatic way in which a computer program requests a service from the kernel of the operating system it is executed on.
- System call provides the services of the operating system to the user programs via Application Program Interface(API).
- Generally written in C or C++, although some are written in assembly for optimal performance.
- System calls are the only entry point into the kernel system

#### Types Of System Calls

1. Process Control
2. File Management
3. Device Management
4. Information Maintenance
5. Communication

### System Programs

- System programs provide OS functionality through separate applications, which are not part of the kernel or command interpreters. also known as system utilities or system applications.
  - File management
  - Status Information
  - File modification
  - Programming language support
  - program loading and execution
  - Communications
  - Background Services

### Operating System Structure

For efficient performance and implementation an OS should be partitioned into separate subsystems, each with carefully defined tasks, inputs, outputs, and performance characteristics.

#### Simple Structure

- does not break the system into subsystems, and has no distinction between user and kernel modes.

#### Layered Approach

- to break the OS into a number of smaller layers, each of which rests on the layer below it, and relies solely on the services provided by the next lower layer.
- allows each layer to be developed and debugged independently, with the assumption that all lower layers have already been debugged and are trusted to deliver proper services.
- no layer can call upon the services of any higher layer.
- can be less efficient, as request for service from a higher layer has to filter through all lower layer before it reaches the HW.

#### Microkernels

- the basic idea behind micro kernels is to remove all non-essential services from the kernel, and implement them as system applications instead, making the kernel as small and efficient as possible.
- Security and protection can be enhanced, as most services are performed in user mode.
- System expansion much easier.

#### Modules

- Modern OS development is object-oriented, with relatively small core kernel and a set of modules which can be linked in dynamically.
- Modules are similar to layers in that each subsystem has clearly defined tasks and interfaces, but any module is free to contact any other module, eliminating the problems of going through multiple intermediary layers.
- Kernel is relatively small in the architecture, similar to microkernels, but the kernel does not have to implement message passing since modules are free to contact each other directly.

#### Hybrid Systems

OS that do not strictly adhere to one architecture, but are hybrids of several.

##### Mac OS X

- relies on the Mach microkernel for basic system management services, and the BSD kernel for additional services.
- Application services and dynamically loadable modules ( kernel extensions ) provide the rest of the OS functionality.

### Operating System Debugging

- Application failures can generate core dump file capturing memory of the process
- Operating system failure can generate crash dump file containing kernel memory

### System Boot

the general approach when most computers boot up goes something like this:

1. system powers up
2. an interupt is generated which loads a memory address into the program counter, and the system begins executing instructions found at that address.This address points to the bootstrap program located in ROM/EPROM chips on the motherboard.
3. ROM bootstrap run hardware checks. Determining what physical resources are present and doing power on self tests(POST) of all HW for which this is applicable. Some devices, such as controller cards may have their own on-board diagnostics, which are called by the ROM bootstrap program.
4. user has the option to run ROM BIOS config utility during POST process. allows user to configure certain hardware parameters.
5. bootstrap program looks for a non-volatile storage device containing an OS.
6. Assuming it goes to a hard drive, it will find the first sector on the hard drive and load up the fdisk table, which contains info about how the physical hard drive is divided up into logical partitions.
7. There is also a very small amount of system code in the portion of the first disk block not occupied by the fdisk table. This bootstrap code is the first step that is not built into the hardware, i.e. the first part which might be in any way OS-specific. Generally this code knows just enough to access the hard drive, and to load and execute a ( slightly ) larger boot program.
8. for **single-boot** system, the boot program will locate the kernel on the hard drive, load the kernel into memory, then transfer control over to the kernel.
9. for **dual-boot** or **multiple-boot** systems, the boot program will give user opportunity to specify a particular OS to load(with default choice). the boot program then finds the boot loader for the chosen single-boot OS,and procede as described in #8.
10. Once the kernel is running, user has the opportunity to enter single-user mode, also known as maintenance mode. this is used primarily for system maintenance and diagnostics.
11. when the system enters full multi-user multi-tasking mode, it examines configuration files to determine which system services are to be started,and launches each of them in turn.
12. Launch login programs (gettys) on each of the login devices which have been configured to enable user logins.
    - The getty program initializes terminal I/O
    - issues login prompt
    - accept login names and passwords
    - authenticates the user
    - if user is authenticated, then the getty looks in system files to determine what shell is assigned to the user, and then "execs" ( becomes ) the user's shell.
    - shell program look in system and user config files to initialize itself, and then issue prompts for user commands.
    - Whenever the shell dies, the system will issue a new getty for that terminal device.

## Processes

### Concept

- process is an instance of a program in execution.
- Batch system work in terms of "jobs".

#### The Process

Process memory is divided into four sections

- **text** => contain the compiled program code
- **data** => stores global and static variable
- **heap** => used for dynamic memory allocation, and is managed via calls to new, delete, malloc, free, etc.
- **stack** => space on stack is reserved for local variables , the space will then freed up when the variable go out of scope.

stack and heap start at the opposite ends of the process's free space and grow towards each other. if they should ever meet, then **stack overflow** error will occur.

#### Process State

- **New** => at the stage of being created.
- **Ready** => has all the resources it needs, but CPU is not currently working on this
- **Running** => CPU is working on it
- **Waiting** => waiting for some resources to be available or some event to occur.
- **Terminated** => Process completed.

#### Process Control Block(PCB)

for each Process there is a PCB which stores the following

- Process State
- Process ID
- CPU registers and Program Counter
- CPU-Scheduling information - such as priority information and pointers to scheduling queue.
- Memory-Management information
- Accounting Information - user and kernel CPU time consumed, account numbers, limits
- I/O Status information

### Process Scheduling

- has 2 objective = keep the CPU busy at all time and deliver acceptable response times for all program
- must meet this objectives by implementing suitable policies for swapping processes in and out of the CPU.

#### Scheduling Queues

- All process are stored in the job queue.
- Ready process are in **ready queue**
- Process waiting for a device to become available or to deliver data are placed in device queues.
- Other queues may also be created and used as needed.

#### Schedulers

- **long-term scheduler** - typical of a batch system or a very heavily loaded system. It runs infrequently, and can affor to take time implementing intelligent and advanced scheduling algorithms.
- **short-term scheduler** - or CPU Scheduler, runs very frequently, on the order of 100 miliseconds, and must very quickly swap one process out of the CPU and swap in another one.
- **medium-term scheduler** - when system loads get high this scheduler will swap one or more processes out of the ready queue system for a few seconds, in order to allow smaller faster jobs to finish up quickly and clear the system
- an efficient scheduling system will select a good process mix of CPU-bound process and I/O bound process

#### Context Switch

- Whenever an interrupt arrives, the CPU must do a state-save of the currently running process, then switch into kernel mode to handle the interrupted process.
- When CPU switches to another process, the system must save the state of the old process (to PCB) and load the saved state (from PCB) for the new process via a **context switch**.
- **context switch** occurs when the time slice for one process has expired and a new process is to be loaded from the ready queue. will be instigated by a timer interrupt, which will then cause the current process's state to be saved and the new process's state to be restored.
- saving and restoring states involves saving and restoring all of the registers and program counter(s) as well as the PCB
- happen VERY frequently, and the overhead the switching is just lost CPU time, so context switch needs to be fast.
- some hardware has multiple sets of registers, so the context switching can be speeded up by switching set of registers are currently in use

##### Multitasking in Mobile System

- early version did not provide user-app multitasking, one app running others are suspended
- **foreground** application is the app currently appearing on display
- **background** app remains in memory but does not occupy the display screen
- CPU can support multitasking, but Apple choose not to to manage resource use(battery life and memory use)
- Android does not place such constraints on the types of app that can run in the background.
- if an app require processing while in the background, the app must use a **service**(a separate app component that runs on behalf of the background process)
- for example when playing music, when music player moves to background, the **service** continues to send audio files to the audio driver on behalf of the background app. the service will continue to run even if the background app is suspended.
- **Service** do not have a UI and have small memory footprint

### Operation on Process

#### Process Creation

- Processes may create other process through system calls, such as **fork** or **spawn**. the creator process is **parent** and the created is **child**
- each process has **PID**. parent PID(PPID) is also stored for each process.
- On UNIX, the **sched**(process scheduler) is given PID 0. the first thing it does at startup time is to launch **init**, which is PID 1. **Init** launch all system daemons and user logins, and become the ultimate parent of all processes.
- Depending on system implementation, Parents and children can share all/some/none resources
- there are 2 options for parent after creating child:
  - wait for the child to terminate before proceding(`wait()` system call).
  - run concurrently with the child, continuing without waiting. this is the operation seen when UNIX runs a process as a background task. its possible to run for a while and wait() later.

#### Process Termination

- may request their own termination using **exit()** returning an int. this int is passed to parent if it is in `wait()`, is zero if successful completion and non-zero if theres problem.
- Process may also be terminated by the system for reasons, including:
  - the inability of the system to deliver necessary system resources.
  - KILL command
  - parent kill its children if the task is no longer needed.
  - if parent exits, system may or may not allow child to continue.
- when a process terminates, all of its system resources are freed up
- process termination status and execution times are returned to the parent if the parent is waiting, or to the init if its an orphan.
- process which are trying to terminate but which cannot because their parent is not waiting for them are termed **zombies**.

### Interprocess Communication

- **Independent Processes** operating concurrently on a systems are those that can neither affect other process or be affected by other process.
- **Cooperating Process** are those that can affect or be affected by other process. reasons why its allowed:
  - Information sharing - often a solution to a problem can be broken down into sub-tasks to be solved simultaneosly.
  - Modularity - the most efficient architecture may be to break a system down into cooperating modules.
  - convenience
- cooperating process requires inter-process communication, which has 2:
  - Shared Memory
  - Message Passing

#### Shared-Memory Systems

- Shared Memory is faster once it is setup, because no system calls are required and access occurs at normal memory speeds. However, is more complicated to set up, and doesn't work as well across multiple computers. Preferable when large amount of information must be shared quickly on the same computer.
- there are two Processes: **Producer** and **Consumer**. both share a common space or memory location known as buffer where the item produced by Producer is stored and from which the Consumer consumes the item.
- In general the memory to be shared is initally within the address space of a particular process, which needs to make system calls in order to make that memory publicly available to one or more other processes.
- other process need to make their own system calls to attach the shared Memory area onto their address space.
- a few messages must be passed back and forth between the cooperating processes first in order to set up and coordinate the shared memory access.
- data is passed via intermediary buffer which may be either unbounded or bounded.
- **bounded buffer** the producer may have to wait until there is space in buffer
- **undbounded buffer** the producer will never have to wait because there is no limit on the size of the buffer.

#### Message-Passing Systems

- requires system calls for every message transfer, and is therefore slower, and opposite to shared Memory in many ways. preferable when the amount of data transfer is small or when multiple computers are involved.
- there are three key issues to be resolved in message passing systems as further explored in the next three subsections:
  - Direct or indirect communication ( Naming )
  - Synchronous or asynchronous communication
  - Automatic or explicit buffering

##### Naming

- with **direct communication** the sender must know the name of the receiver.
  - there is a one-to-one link between every sender-receiver pair
  - for **symmetric** communication, the receiver must also know the specific name of the sender from which it wishes to receive messages. for **asymmetric** this is not necessary.
- **Indirect communications** uses shared mailboxes(ports).
  - only one process can read any given message in a mailbox. Initially the process that creates the mailbox is the owner, and is the only one allowed to read mail in the mailbox, although the priviledge may be transferred.
  - the OS must provide system calls to create and delete mailboxes, and to send and receive messages to/from mailboxes.
  -

##### Synchronization

- Either the sending or receiving of messages(or neither or both) may be either **blocking** or **non-blocking**.

##### Buffering

- messages are passed via queues, which may have one of three capacity configuration:
  - Zero capacity - Messages cannot be stored in the queue so senders must block until receivers accept the messages.
  - Bounded capacity - there is a certain pre-determined finite capacity in the queue. senders must block if the queue is full, until space becomes available in the queue, but may be blocking or non-blocking
  - Unbounded-capacity - the queue has a theoratical infinite capacity, so senders are never forced to block.

### Example of IPC Systems

#### POSIX

<!--  will add later -->

#### Mach

- most communication including all system calls and IPC is done via messages sent to mailboxes, also known as ports.
- Whenever a task(process) is created, it automatically get two special mailboxes:
  - **Kernel mailbox** - kernel use this to communcates with the task
  - **Notify Mailbox** - kernel sends notification of events to Notify mailbox
- Only one task at a time can own or receive messages from any given mailbox, but these are transferable.
- Messages from the same sender to the same receiver are guaranteed to arrive in FIFO order, but no guarantees are made regarding messages from multiple senders.
- if the receiver's mailbox is full, the sender has four choices:
  1. Wait indefinitely until there is room in the mailbox.
  2. wait at most N miliseconds.
  3. Do not wait at all.
  4. Temporarily cache the message with the kernel, for delivery when the mailbox become available.
  - only one such message can be pending at any given time from any given sender to any given receiver.
  - Normally only used by certain system tasks, such as the print spooler, which must notify the client of the completion of their job, but cannot wait for the mailbox to become available.
  - Receive calls must specify the mailbox or mailbox set from which they wish to receive messages.

### Communication in Client-Server Systems

#### Sockets

- socket is an endpoint for communication
- two process communication over a network often use a pair of connected sockets as a communication channel.
- may also use sockets for communication between two processes running on the same computer.
- a socket is identified by an IP address concatenated with a port number, e.g. 200.100.50.5:80.
- port numbers below 1024 are considered to be _well-known_, and are generally reserved for common internet services.
- General purpose user sockets are assigned unused port over 1024 by the OS in response to system calls such as socket() or socketpair().
- Communication channels via sockets may be one of two major forms:
  - **Connection-oriented**(TCP, **Transmission Control Protocol**)
    - emulate a telephone connection
    - designed to send packets across the internet and ensure the successful delivery of data and messages over network.
    - all packets sent down the connection are guaranteed to arrive in good condition at the other end, and to be delivered to the receiving process in the order in which they were sent.
    - takes step to verify all packets sent, re-send packets if necessary, and arrange the received packets in the proper order before delivering them to the receiving process.
    - if one packet is missing or delayed, then any packets which follow will have to wait until the errant packet is delivered
  - **Connectionless**(UDP, **User Datagram Protocol**)
    - emulate individual telegrams.
    - no guarantee that any packet will get through undamaged and delivered in any particular order.
    - may even duplicate packets
    - faster than TCP
    - app must implement own error checking and recovery procedures to use it
- Sockets are considered low-level communications channels.

#### Remote Procedure Calls,RPC

- the general concept is to make procedure calls similarly to calling on ordinary local procedures, except the procedure being called lies on a remote machine.
- Implementation involves **stubs** on either end of connection:
  - local process calls on stub, as it would call upon a local procedure.
  - RPC System packages up the parameters to the procedure call and transmit them to the remote system.
  - on remote side, RPC daemon accepts the parameters and calls upon the appropriate remote procedure to perform the requested work.
  - results returned are packaged up and sent back to the local system, which then unpackages them and returns results to the local calling procedure.
- the difficulty is the formatting of data on local versus remote systems. the resolutions of this problem generally involves an agreed-upon intermediary format, such as **XDR**(**external data representation**).
- another issue is identifying which procedure on the remote system a particular RPC is destined for.
  - Remote procedures are identified by _ports_,(not the same with socket ports)
  - one solution is for the calling procedure to know the port number they wish to communicate with on the remote system. this is Problematic, as the port number would be compiled into the code, and it makes it break down if the remote system changes their port numbers.
  - a _matchmaker_ process is employed, that acts like a telephone directory service. local process must first contact the matchmaker on the remote system which looks up the desired port number and returns it. local process can then use that information to contact desired remote procedure. this operation involves an extra step but is much more flexible.

#### Pipes

- are one of earliest and simplest channels of communications between (UNIX) process.
- Data is entered from one end of the Pipe by a process and consumed from the other end by the other process.
- four key considerations in implementing pipes:
  - Uni- or Bi-directional communication?
  - is Bidirectional communication half-duplex or full-duplex?
  - Must a relationship such as parent-child exist between the process?
  - can pipes communicate over network, or only on the same machine?
- two types of pipes:
  - **ordinary**
    - only allow one way communication
    - have a parent child relationship between the processes as the pipes can only be accessed by process that created or inherited them.
  - **Named**
    - are more powerful than ordinary pipes and allow two way communication
    - exist even after the processes using them have terminated.
    - need to be explicitly deleted when not required

## Threads

### Overview

- _thread_ is a basic unit of CPU utilization, consisting of a program counter, a stack, and a set of registers(and thread ID).

#### Process vs Thread

- threads within the same process run in a shared memory space, while processes run in separate memory spaces.
- threads are not independent of one another like processes are, it share with other threads their code section, data section, and OS resources.
- but has its own PCB, register set, and stack space.

#### Motivation

- thread are useful in modern programming whenever a process has multiple tasks to perform independently of the others.
- when one of the tasks may block, and it is desired to allow the other tasks to proceed without blocking.
- for example in web server:
  - threads allows for multiple requests to be satisfied simultaneously, without having to service requests sequentially or to fork off separate processes for every incoming request.

#### Benefits

- Responsiveness
- Resource sharing
- economy
- scalability

### Multicore Programming

- a recent trend in computer architecture is to produce chips with multiple cores, or CPUs on a single chip.
- for operating systems, multi-core chips require new scheduling algorithms to make better use of the multi-cores availble.

#### Programming Challenges

For application programmers, there are five areas where multi-core chips present new challenges:

- **Identifying tasks** - Examining apps to find activities that can performed concurrently.
- **Balance** - Finding tasks to run concurrently that provide equal value.
- **Data Splitting** - to prevent the threads from interfering with one another.
- **Data dependency** - if one task is dependent upon the results of another, then the tasks need to be synchronized to assure access in the proper order.
- **Testing and debugging** - Inherently more difficult in parallel processing situations, as the race conditions become much more complex and difficult to identify.

#### Types of Parallelism

in theory there are two different ways to parallelize the workload:

1. **Data parallelism** - divides the data up amongst multiple cores(threads), and performs the same task on each subset of the data.
2. **Task parallelism** - divides the different tasks to be performed among the different cores and perform them simultaneously.

### Multithreading Models

- There are two types of threads to be managed in a modern system: **User** and **Kernel** threads.
- User threads are supported above the kernel, without kernel support. These are the threads that app programmer put into their programs.
- Kernel threads are supported within the kernel of the OS itself. All modern OSes support kernel level threads, allowing the kernel to perform multiple simultaneos tasks and/or to service multiple kernel system calls simultaneously.
- In a specific implementation, the user threads must be mapped to kernel threads, using one of the following strategies.

#### Many-To-One Model

- many user-level threads are all mapped onto a single kernel thread.
- Thread management is handled by the thread library in user space, which is very efficient.
- however, if blocking system call is made, then the entire process blocks, even if the other user threads would otherwise be able to continue.
- Because a single kernel thread can operate only on a single CPU, does not allow individual processes to be split across multiple CPUs.

#### One-to-One Model

- create a separate kernel thread to handle each user thread.
- overcome the problem involving blocking system calls and the splitting of processes across multiple CPUs.
- However, the overhead of managing the one-to-one model is more significant, involving more overhead and slowing down the system.
- most implementation place a limit on how many threads can be created.
- Linux and Windows from 95 to XP implement the one-to-one model for threads.

#### Many-to-Many Model

- multiplexes any number of user threads onto an equal or smaller number of kernel threads, combining the best features of the one-to-one and many-to-one models.
- Users have no restrictions on the number of threads created.
- Blocking kernel system calls do not block the entire process.
- Processes can be split across multiple processors.
- Individual processes may be allocated variable numbers of kernel threads, depending on the number of CPUs present and other factors.

### Thread Libraries

- thread libraries provide programmers with an API for creating and managing threads.
- may be implemented in user or kernel space.
- 3 main thread libraries in use today:
  1. POSIX (Pthreads)
  2. Win32 threads - kernel-level in windows systems
  3. Java threads - the implementation of threads is based upon whatever OS and hardware the JVM is running on(either Pthreads or Win32)

### Threading Issues

#### The fork() and exec() System Calls

- Q: If one thread forks, is the entire process copied, or is the new process single-threaded?
- A: System dependant.
- A: If the new process execs right away, there is no need to copy all the other threads. If it doesn't, then the entire process should be copied.
- A: Many versions of UNIX provide multiple versions of the fork call for this purpose.

#### Signal Handling

- Q: When a multi-threaded process receives a signal, to what thread should that signal be delivered?
- A: four options:
  1. Deliver the signal to the thread to which the signal applies
  2. deliver the signal to every thread in the process
  3. deliver the signal to certain threads in the process
  4. Assign a specific thread to receive all signals in a process
- Unix allows individual threads to indicate which signals they are accepting and which to ignore. however, can only be delivered to one thread, thus given to the first threads that is accepting the signals.
- Unix provides `kill(pid, signal)` and `pthread_kill(tid, signal)` for delivering signals to processes or specific threads respectively.
- Windows does not support signals, but they can be emulated using Asynchronous Procedure Calls. APCs are delivered to threads not processes.

#### Thread Cancellation

- threads that are no longer needed may be cancelled by another thread in one of two ways:
  1. **Asynchronous Cancellation** cancels the thread immediately.
  2. **Deferred Cancellation** sets a flag indicating the thread should cancel itself when its convenient.
- (Shared) resource allocation and inter-thread data transfers can be problematic with async cancellation.

#### Thread-Local Storage

- Most data is shared among threads, and this is one of the major benefits of using threads in the first place.
- However threads sometimes need thread-specific data.
- Most thread libraries(pThreads,Win32, Java) provides support for thread-specific data known as thread-local storage or TLS. this is more like static data than local variables, because it does not cease to exist when the function ends.

#### Scheduler Activations

<!-- REVIEW THIS LATER -->

- many implementations of threads provide a virtual processor as an interface between the user thread and the kernel thread, particularly for the many-to-many or two-tier models.
- virtual processor is known as a "lightWeight Process", LWP.

**Scheduler** activations provide upcalls – a communication mechanism from the kernel to the thread library.

- Allows application to maintain the correct number of kernel threads

## Process Synchronization

- there are a number of processes present in a particular state.
- At the same time, we have a limited amount of resources present, which need to be shared among the processes.
- but, there should be no two processes are using the same resource at the same time because it will lead to data inconsistency.
- Processes that are sharing resources between each other are called **Cooperative Processes** and processes whose execution does not affect the execution of other processes are called **Independent Processes**.

### Race Condition

- In OS, we have a number of processes and these processes require a number of resources.
- race condition is condition happen when 2(or more) process are using the same resource at the same time
- during simultaneous execution, the modification of the shared variable from one process will effect the execution result of the other process who shared the variable. which leads to undesired result.
- is difficult to debug because it occur on rare occasions and when the timing is right(or wrong) and very difficult to reproduce.
- the solution is to allow one process at a time to manipulate the shared variable.

### Critical-Section Problem

- in a number of cooperating processes, each has a critical section of code, with the following conditions and terminologies:
  - Only one process in the group can be allowed to execute in their critical section at any one time. other process will have to wait for their critical process to execute until the critical of the current process finish executing.
  - the code preceding the critical section, and which controls access to the critical section, is termed the **entry section**. acts like a carefully controlled locking door.
  - the code following the critical section is termed the **exit section**. it lets the other know that they are no longer in critical section.
  - the rest of code that is not critical, entry or exit is called the **remainder section**.
- A solution to the critical section problem must satisfy the following three conditions:
  1. **Mutual Exclusion** - Only one process at a time can be executing in their critical section.
  2. **Progress** - If no process is currently executing in their critical section, and one or more processes want to execute their critical section, then only the processes not in their remainder sections can participate in the decision. and the decision cannot be postponed indefinitely.
  3. **Bounded Waiting** - There exists a limit as to how many other processes can get into their critical sections after a process requests entry into their critical section and before that request is granted.
- We assume that all processes proceed at a non-zero speed, but no assumptions can be made regarding the relative speed of one process versus another.
- Kernel processes can also be subject to race conditions, which can be especially problematic when updating commonly shared kernel data structures such as open file tables or virtual memory management. Accordingly kernels can take on one of two forms:
  - **Non-preemptive** kernels do not allow processes to be interrupted while in kernel mode. eliminates the possibility of kernel-mode race conditions, but requires kernel mode operations to complete very quickly, can be problematic for real-time systems because timing is not guaranteed.
  - **Preemptive** kernels allow for real-time operations, but must be carefully written to avoid race conditions.

### Peterson's Solution

- is a classic software-based solution to the critical section problem.
- not guaranteed to work on modern hardware, due to vagaries of load and store operations.
- Peterson's solution is based on two processes, which alternate between their critical sections and remainder sections.
- Peterson's solution requires two shared data items:
  - int turn - Indicates whose turn it is to enter into the critical section.
  - boolean flag[ 2 ] - Indicates when a process wants to enter their critical section.

### Synchronization Hardware

<!-- USUALLY DISCUSSED ON ADVANCED BOOKS -->

- One simple solution to the critical section problem is to prevent a process from being interupted while in their critical section.
- but wont work on multiprocessor environments due to difficulties in disabling and re-enabling interrupts on all processors.
- another approach is for **hardware to provide certain atomic operations**.
- these operations are guaranteed to operate as a single instruction, without interruption.

### Mutex Locks

- in this approach, in the entry section of code, a LOCK is acquired over the critical resources modified and used inside the critical section, and in exit section the LOCK released.
- one problem with this implementation is the busy loop used to block processes called **spinlocks** because CPU just sit and spin while blocking the process.
- Spinlocks are wasteful of cpu cycles, and are a really bad idea on single-cpu single-threaded machines.
- On the other hand, spinlocks do not incur the overhead of a context switch, so they are effectively used on multi-threaded machines when it is expected that the lock will be released after a short time.

### Semaphores
