# Operating System

Some of the important activities that an OS performs
- **Security** - prevent anauthorized access to program and data
- **Control Over System Performance** - Recording delays between request for a service and response from the system
- **Job Accounting** - Keeping track of time and resources used by various jobs and resources
- **Error detecting aids**
- **cordination between other softwares and users** - Coordination and assignment of compilers, interpreters, assemblers and other software to the various users of the computer systems.

## Computer System Architecture
### Single-Processor Systems
one CPU one processing core.

NOTE: **core** is the component that executes instructions and registers for storing data locally.

### Multiprocessor Systems
have two or more processors each with single-core CPU.

share the computer bus (and sometime clock, memory and peripheral devices).

**multicore** multiple computing core in one chip.

#### Symmetric Multiprocessor(SMP)
each CPU processor performs all tasks(inculding OS and User Process)

each has its own set of registers and private and local cache.

share physical memory over system bus.

Multicore systems can be more efficient than multiple chips with single cores
because on-chip communication is faster than between-chip communication.

**NUMA** systems can scale to accommodate a large number of processors.

### Clusters System
Another type of Multiprocessor.

two or more individual systems(nodes) joined together with each is a multicore system.

generally accepted definition: share storage and linked via LAN or faster interconnect.

provide services that will continue even if one or more systems fail(high-availability service).

asymmetric or symmetric.

greater computational power
than single-processor or SMP systems.

## Operating System Operation

### Multiprogramming
OS keeps several processes in memory, pick one and execute, eventually the process will wait for some task. in a non-multiprogrammed, CPU will sit idle. In a multiprogrammed system, switches to and executes, another process.

**Multitasking** systems, the CPU executes multiple processes by switching among them, but the switches occur frequently, providing the user with a fast response time.

if several process are ready to run at the same time, **CPU Scheduling** will choose which run next.

### Dual mode and Multimode
user mode and kernel mode.

designating some of the machine instructions
that may cause harm as **privileged instructions**.

### Timer
prevent user program to stuck in infinite loop or to fail to call system services and never return control to the operating system.

ensures that no process can gain control of the CPU without eventually
relinquishing control.

## Virtualization
a technology that allows us to abstract the hardware of a single computer (the CPU , memory, disk drives, network interface cards, and so forth) into several different execution environments.

allows OS to run within another OS.

## Kernel Data Structure
### List Stacks and Queues
Whereas each item in an **array** can be accessed directly, the items in a list must be accessed in a particular order.

**list** represents a collection of data values as a sequence. (common method implementing this is **linked list**)

types linked lists:-
- singly linked
- doubly linked
- circularly linked

**stack** is a sequentially ordered data structure that uses the **last in, first out** principle.

OS use stack when invoking function calls.

**Queue** like stack but **first in, first out**

### Trees
used to represent data hierarchically.

### Hash Functions and Maps
**hash function** takes data as its input, performs a numeric operation on the
data, and returns a numeric value.

One use of a hash function is to implement a hash map, which associates (or maps) [key:value] pairs using a hash function.

### Bitmaps
a string of <i>n</i> binary digits that can be used to represent the status of
<i>n</i> items.


## Overview
- some of importance functions of OS:
- Memory Management
- Processor Management
- Device Management
- File Management
- Security
- Control over system performance
- Job accounting
- Error detecting aids
- Coordination between other software and users

## Memory Management
refers to management of Primary Memory or Main Memory.

OS does these for memory management -
- keeps tracks of primary memory
- decide which process get memory(and how much)
- Allocates the memory
- De allocates the memory

## Processor Management
in multiprogramming, OS decides which process gets the processor when and how long.

## Device Management
OS manage device communication via their respective drivers.
## File Management
A file system is normally organized into directories for easy navigation and usage.

## Types of OS
### Batch OS
users do not interact directly with the computer.

each user prepares his job on an off-line device like punch cards and submits it to the computer operator.

similar needs are batched together and run as group(for speed).

problem with the OS:
- Lack user and job interaction
- CPU often idle (speed of mechanical I/O is slower)
- Difficult to provide the desired priority.

### Time-sharing OS
enables many people, located at various terminals, to use a Computer System at same time.

Processor's time is share to multiple users simultaneously(time-sharing).

minimized response time.

Multiple jobs are executed by the CPU by switching between them(time quantum).

OS uses **CPU scheduling** and **multiprogramming** to provide each user with a small portion of a time.

better than Batch OS.

avoid duplication of software.

Reduce idle.

Disadvantages:
- Problem of reliability.
- Question of security and integrity of user programs and data.
- Problem of data communication.

### Distributed OS

A distributed system is a collection of physically separate, possibly heterogeneous computer systems that are networked to provide users with access to the various resources that the system maintains

use multiple central processors to serve multiple real-time applications and multiple users.

processors communicate with one another through communication lines(i.e high speed buses or telephone lines) that are refered to as **loosely coupled system** or distributed systems.

these processors are refered to  as sites, nodes, computers ...etc.

Processors may vary in size and function.

advantages:-
- a user at one site may be able to use the resources available at another
- speed up the exchange of data within users
- if one sites fails, no effect on other
- reduction of load on the host computer
- reduction of delays in data processing

types of Network:
- **Local Area Network(LAN)** room size
- **Wide-area Network(WAN)** usually links buildings, cities, or countries
- **Metropolitan-area Network(MAN)** link buildings within a city
- **Personal-area Network** bluetooth and 802.11 devices

### Network OS
 runs on a server and provides the server the capability to manage data, users, groups, security, applications, and other networking functions.

allow shared file and printer access among multiple computers in a network, a local area network (LAN), a private network or to other networks.

advantages:-
- Centralized server are stable
- Security is server managed
- easy to upgrade
- remote access is possible(diffrent location and types of system)

disadvantages:
- expensive
- Dependency on a central location(most operations)
- regular maintenace required

### Real Time OS
defined as a data processing system in which the time interval required to process and respond to inputs is so small that it controls the environment.

**Response Time**(time taken by the system to respond to an input and display of required updated information).

used when there are rigid time requirements on the operation of a processor or the flow of data and real-time systems can be used as a control device in a dedicated application.

must have well-defined, fixed time constraints, otherwise the system will fail.

two types of this OS

#### Hard
guarantee that critical tasks complete on time.

secondary storage is limited or missing and the data is stored in ROM.

no virtual memory(almost).

#### Soft
critical real-time task gets priority over other tasks and retains the priority until it completes.

limited utility than hard real-time systems.(multimedia, virtual reality, Advanced Scientific Projects like undersea exploration and planetary rovers)

## Services
- Program execution
- I/O operations
- File System manipulation
- Communication
- Error Detection
- Resource Allocation
- Protection

## OS Properties
### Batch processing
collects the programs and data together in a batch before processing starts.

### Multitasking
multiple jobs are excecuted by the CPU simultaneously by switching between them.

uses the concept of CPU scheduling and multiprogramming.

take advantage of slow I/O interaction of process.

### Multiprogramming
Sharing the processor, when two or more programs reside in memory at the same time.

CPU scheduling and Memory Management required.

### Interactivity
the ability of users to interact with a computer system.

OS provides the UI.

response time needs to be short, since user submit and waits for the results.

### Real Time System
read from and react to sensor data.

must guarantee response to events for correct performance.

### Distributed Environment
multiple independent CPUs or processors in a computer system.

no memory and clock sharing.

OS manage communication between processors.

### Spooling
acronym for **S**imultaneous **P**eripheral **O**perations **O**n **L**ine.

putting data of various I/O jobs in a buffer(a special area in memory or hard disk accessible to I/O devices).

Handles I/O device data spooling as devices have different data access rates.

OS maintains Spooling buffer(a waiting station where data can rest while slower device catches up).

It becomes possible to have the computer read data from a tape, write data to disk and to write out to a tape printer while it is doing its computing task.

## Process
basically a program in execution in a sequential fashion.

When a program is loaded into the memory and it becomes a process, it can be divided into four sections ─ stack, heap, text and data.

**Stack** ― temporary data such as method/function parameters, return address and local variable
**Heap** ― dynamically allocated memory to a process during its run time
**Text** ― current activity(program Counter Value), processor's register content
**Data** ― global/static variables

## Program
A computer program is a collection of instructions(programming languages) that performs a specific task when executed by a computer.

process is a dynamic instance of a program.

 A collection of computer programs, libraries and related data are referred to as a **software**.