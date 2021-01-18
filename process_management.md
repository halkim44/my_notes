# Process Management

## The Process
is a program in execution.

the current activity of a process is represented by the value of the**program counter** and the content of processor's registers.

memory layout of a process:
- text
- Data
- Heap
- Stack

sizes of text and data section are fixed, stack and heap can shrink and grow dynamically during execution.

process is and active entity with a program counter specifying the next instruction to execute and a set of associated resources.

a **program** is not process, its a passive entity(executable file).

two process may be in same program, but still considered two separate execution sequences (although the text sections are equivalent, the data, heap, and stack sections vary).

### Process state
states:
- New
- Running
- Waiting
- Ready

### Process Control Block(PCB)
contains pieces of information associated with a specific process:
- Process State
- Program Counter
- CPU Register - accumulators, index registers, stack pointers, and general-purpose registers, plus any condition-code information. along with program counter, helps when an interupts occurs.
- CPU Scheduling information
- Memory Management information
- Accounting information - the amount of CPU and real time used, time limits, account numbers, job or process numbers ...
- I/O Status Information - list of I/O devices, list of open files ...

### Threads
A multithreaded word processor could, for example, assign one thread to manage user input while another thread runs the spell checker.

PCB is expanded to include information for each threads.

## Process Scheduling
helps in **multiprogramming** and **time-sharing**.

if there are more processes than cores, excess processes will have to wait until a core is free and can be rescheduled.

The number of processes currently in memory is known as the **.degree of multiprogramming**.

mostprocesses can be described as either **I/O bound**(more I/O than computation) or **CPU bound**(more computation, generate I/O req infrequently).

### Scheduling Queues
**Ready queue**
- process ready and waiting to be executed
- generally stored as a linked list
- ready-queue header have pointer to first PCB(that has pointer field to the next PCB and so on..)

**Wait Queue**
- processes waiting for certain event to occurs(I/O) are placed here

theres a queueing-diagram.

once a process is allocated a CPU core and is executing, the process could:
- issue an I/O request and placed in I/O wait queue
- create a new child process and placed in wait queue waiting the child's termination
- be removed from core(interupts or time slice expires) and go to ready queue

A process continues this cycle until it terminates, at which time it is removed from all queues and has its PCB and resources deallocated.

### CPU Scheduling

select from among the processes that are in the ready queue and allocate a CPU core to one of them.

unlikely to grant the core to a process for an extended period and can forcibly remove the CPU from a process and schedule another process.

CPU scheduler executes at least once every **100 milliseconds**.

there are also **swapping** scheduling. a process can be swapped out from memory to disk, where its current status is saved, and later "swapped in" from disk back to memory.

### Context Swith
interrupts cause the operating system to change a CPU core from its current task and to run a kernel routine.

when interupts occurs, save the current context of the process running so that it can be restored.

the **context** is represented in the PCB of the process.

state save and then state restore.

**context switch** - Switching the CPU core to another process requires performing a state save of the current process and a state restore of a different process.

## Operation on Processes
### Process Creation
theres a **tree** of process.

OS identify process using **pid**(typically integer). it provide a unique value and as an index for each process.

when a process create a child process, restricting a child process to a subset of
the parent’s resources prevents any process from overloading the system by creating too many child processes.

when a process create a new process, the parent can:
- execute concurrently with its children
- wait until some or all children terminates

address-space possibilities for the new process:
- child is duplicate of parent process
- child has new program

A new process is created by the ``fork()`` system call.(Windows use ``CreateProcess()`` but has parameters for inheritance)

child has copy of address space of parent for easy communication.

parent ``wait()`` for the child to explicit/implicit-ly call ``exit()`` and will receive exit status.
``exec()`` loads a binary file into memory(destroying the memory of the program that calls it) and start its executions.

### Process Termination
when process calls ``exit()``.

child will return **status value** to parents with ``wait()``. all resources of the process will be deaollocated by OS.

only parents can cause the termination of others(only its child). because the identity of child process is passed to parent upon creation, parent can use it to delete that child.

reason a parent terminate a child:
- exceeded usage of resources
- task assigned no longer required
- OS dont allow child to continue if parent terminated(**cascading termination**).

when child process terminated, it will be in the process table until the parent calls ``wait()``because the process table contains the process’s exit status. this is called zombie process.

when parent terminate while still have zombie, the zombie become orphans and ``init```` or ``systemd`` will be parent(because it is root it will call ``wait()`` eventually, exiting the orphan).

#### Android Process Hierarchy
uses **importance hierarchy** means terminating process in order of increasing importance(usually to make way for new or more important process).

hierarchy classifications(most to least importance):
- process is visible on screen(foreground)
- process that performing activies whose status is visible on foreground process
- service process(like listening to music on the background)
- Background process
- process that hold no active component associated with any application.

theres a guide line of **process life cycle** for android development practices.

## Interprocess Communication(IPC)
**independent process** ― don't share data with any other process executing in the system

**cooperating process** ― if a process can affect or be affected by other process executing in the system(and also shared data)

reason for cooperation:
- information sharing to allow concurrent access with the same information
- Computational speedup that is achieved only if the with parallel execution
- Modularity

2 fundamental models of IPC:
- **shared memory**

- **message passing** ― useful for small amount data. easier to implement in distributed system than shared memory.slower than shared memory because is implemented using system calls.

### Google Chrome's Multiprocess architecture
if on tab in a browser crash, all process crash too. Chrome use multiprocess architecture to address this issue.

Chrome identifies 3 types of processes:
- **browser** ― manage UI, disk and network I/O. only one created that is **when Chrome start**.
- **Renderer** ― contain logic for rendering web pages(html, JS, images ..). one created for **each tab created**.
- **Plug-in** ― for each plug-in in use.

Chrome's Multiprocess advantage:
- website run in isolation(if one website crash only its renderer process is affected)
- renderer process run in **sandbox**(access to disk and Network I/O is restricted)

### IPC Shared Memory
process exchange information by read/write data to a shared **region of memory**. implement system calls only to establish shared-memory region.

shared memory region resides in address space of process creating the shared-memory segment. Other process want to communicate using this must attach it to their address space(requires the two process to agree to remove restriction against memory sharing).

To allow **producer** and **consumer** (for example producer is server and consumer is browser) processes to run concurrently, we must have available a buffer of items that can be filled by the producer and emptied by the consumer. this buffer reside in a shared memory.

producer and consumer must be **synchronized**, so that the consumer does not try to consume an item that has
not yet been produced.

2 types of buffer:
- **unbounded buffer** ― no size limit
- **bounded buffer** ― fixed buffer size. producer may wait if full.

the code for accessing and manipulating the shared memory be written explicitly by the application programmer.

### IPC in Message passing
allow processes to communicate and to synchronize their actions without sharing the same address space.

a **communication link** must exist between process. several methods for logically implementing a link:
- Direct/indirect communication
- Synchronous or asynchronous communication
- Automatic or explicit buffering

#### Naming
under **direct communication**, each process that wants to communicate must explicitly name the recipient or sender.

the properties of the communication link:
- link is established automatically between process that want to communicate. they just need to know each other's identity.
- a link for two process
- two process one link

there are two variant symmetry(both must name to connect) and asymmetry(only sender name the recipient). the disadvantage in both of these scheme is when changing the identifier, all reference must to the old identifier must be find and changed too.

with **indirect communication**, the message is sent to and received from **mailboxes** or ports that has unique identity.

the properties of the communication link:
- a link is only established when both have a shared mailbox
- more than two process for a link
- two process many link with each corresponding to one mailbox

methods for choosing which process to execute ``receive()`` when a process sends a message to mailbox:
- allow a link to be associated with two process at most
- allow at most one at a time to execute ``receive()``
- allow the system to select

mailbox owned by process:
- mailbox part of address space
- owner can only receive, user can only send
- when owner terminates, mailbox disappeared and user must be notified

mailbox owned by OS provide a mechanism that allow process to:
- Create mailbox
- send/receive message through mailbox
- delete mailbox

ownership and receiving privilege on a mailbox **can be passed** to other process.

#### Synchronization
communication between processes is by calls to ``send()`` and ``receive()`` primitives.

options for implementing each primitives for message passing is either **blocking** or **nonblocking**.

### Buffering
direct or indirect, messages exchanged by communicating processes reside in a **temporary queue**.

- **Zero capacity** ― cannot have any messages waiting in it. sender block until recipient receives the messages
- **Bounded Capacity** ― has finite length queue. sender can continue when not full.
- **Unbounded Capacity** ― sender never block(potentially infinite).

## Examples of IPC Systems

### POSIX Shared Memory
is organized using memory-mapped files, which associate the region of shared memory with a file(``shm_open()``).

### Mach OS Message passing
### Windows
modular design OS.

message passing facility is called **.advanced local procedure call ( ALPC )**(similar to remote procedure call(RPC) but optimized and for windows only).

windows use port object to establish and maintain connection between 2 process:
- **connection ports**
- **communication ports**

consist of a pair of private communication ports(client-server and server-client messages)

When ALPC channel created, one of the three message passing technique is chosen:
- small messages(up to 256bytes) ― port's message queue as intermediate storage. messages are copied from one process to another.
- Larger Messages ― must passed through **section object**(shared memory).
- larger than section object ― process read and write directly into address space of client

NOTE: google for Advance local procedure calls in Windows.

ALPC is not part of Windows API. applications invoke standard RPC that is handled directly through ALPC procedure call.

### Pipes
pipe act as conduit allowing 2 process to communicate.

in implementing a pipe, four issue must be considered:
- bidirectional or unidirectional communication?
- is two-way communication allowed(half and full duplex)?
- must relationship exist between process?
- can communicate over network? must it on the same machine only?

#### Ordinary Pipes
the producer writes to one end of the pipe (the **write end**) and the consumer reads from the other end (the **read end**).

one-way communication(unidirectional).

cannot be accessed from outside the process that created it.

parent process create pipes using fork() to communicate with child.

child inherit pipes from parent process.