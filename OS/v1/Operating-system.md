# Operating system

## Introduction

### What is OS

- A collection of software that manages computer hardware and provides services for programs.
- hides hardware complexities
- manage computational resources
- provides isolation and protection
- has privilege access to the underlying hardware

### Major components

- file systems
- scheduler
- device driver

### OS in everyday life

#### Desktop

- linux
- Window
- Mac

#### Embedded

- android
- iOS

### elements of an OS

- Abstraction(process, thread, file, socket, memory)
- Mechanism(create, schedule, open, write, allocate)
- Policies(LRU, EDF)

### Design Principles

- Separation of mechanism and policy
- Optimize for common case

### Types of OS

#### Monolithic

- the entire OS is working in kernel space and is alone in supervisor mode

#### Modular

where some part of the system core will be located in independent files called modules that can be added to the system at run time

#### Micro

where the kernel is broken down into separate processes know as servers(some server run in kernel space, some in user space)

## Process and Process management

- Process = program in execution
- when a program is loaded into memory and become process, it can be divided into four sections
  - stack
  - heap
  - text
  - data

### Stack

contains the temporary data such as method/function parameters, return address and local variables.

### Heap

dynamically allocated memory to a process during its run time.

### Text

includes the current activity represented by the value of Program Counter and the contents of the processor’s registers.

### Data

contains global and static variables.

### Process State

- **Start** : the initial state when a process is first started/created.
- **Ready**
  - process is waiting to be assigned to a processor
  - process may come to this state when interupted by scheduler
- **Running**
- **Waiting** : when it need to wait for a certain resource
- **Terminated**

### Process Control Block (PCB)

- keeps all information needed to keep track of a process
- identified by an integer process ID(PID).
- keep track of the information below:
  - Process State: The current state of the process i.e., whether it is ready, running, waiting, or whatever.
  - Process Privileges: This is required to allow/disallow access to system resources.
  - Process ID: Unique identification for each of the process in the operating system.
  - Pointer: A pointer to parent process.
  - Program Counter: Program Counter is a pointer to the address of the next instruction to be executed for this process.
  - CPU Registers: Various CPU registers where process need to be stored for execution for running state.
  - CPU Scheduling Information: Process priority and other scheduling information which is required to schedule the process.
  - Memory Management Information: This includes the information of page table, memory limits, Segment table depending on memory used by the operating system.
  - Accounting Information: This includes the amount of CPU used for process execution, time limits, execution ID etc.
  - IO Status Information: This includes a list of I/O devices allocated to the process.

## Thread and Concurrency

- thread is a flow of execution through the process code, with its own program counter that keeps track of which instruction to execute next, system registers which hold its current working variables, and a stack which contains the execution history.
- a thread shares a few information with its peer threads(when one thread alters a code segment memory item all other threads see that)
- is also called lightweight process
- provides a way to improve application performance through parallelism.
- each threads represents a separate flow of control.

### advantage of thread

- minimize context switching time
- provides concurrency within a process
- efficient communication
- is more economical to create and context switch threads
- allow utilization of multiprocessor architectures

### Implementation of threads

#### User Level Threads

- thread management kernel is not aware of the existence of threads.
- are small and and much faster than kernel level threads
- there is no kernel involvement in synchronization for user-level threads.

##### Advantage

- Thread switching does not require kernel mode priviledges
- user level thread can run on any OS
- Scheduling can be application specific
- are fast to create and manage

##### Disadvantage

- In a typical OS, most system calls are blocking
- Multithreaded application cannot take advantage of multiprocessing

#### Kernel Level threads

- thread management is done by kernel
- no thread management code in application area
- kernel threads are supported directly by the OS
- any application can be programmed to be multithreaded
- The kernel maintains context information for the process as a whole and for individuals threads within the process
- Scheduling by the kernel is done on a thread basis
- The Kernel performs thread creation, scheduling and management in Kernel space
- kernel threads are generally slower to create and manage than the user thread

##### Advantages

- kernel can simultaneously schedule multiple threads from the same process on multiple processes
- if one thread in a process is blocked, the kernel can schedule another thread of the same process
- Kernel routines themselves can be multithreaded

##### Disadvantages

- slower to create and manage than user threads
- transfer of control from one thread to another within the same process requires a mode switch to kernel.
