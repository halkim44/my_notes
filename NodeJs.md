# Node.js

a Javascript free and open source cross-platform for server-side programming that allows users to build network applications quickly.

## What makes it great

1. runtime is built on **Chrome's V8 js engine**.
2. event-driven, non-blocking I/O model(light weight & efficient)
3. npm

## Event Driven Programming

a computer programming paradigm in which control flow of the program is determined by the occurence of events.

events are monitored by code known as **event listeners**.

## Node Event Loop

- Node Loop will check for events.
- Node loop start the minute you call node

## ExpressJs

its a web framework that lets you structure a web app to handle multiple different http requests at a specific url.

### Why Use Express

- response to requests with routes support
- supports multiple templating engines
- simple and is open source

## What is Cors

**Cross-origin Resource Sharing** is an HTTP-header based mechanism that allows a server to indicate any other origins than its own from which a browsers should permit loading of resources.

## Buffer

Buffer is a mechanism for reading or manipulating streams of binary data.Buffer class was introduced in Node.js API to make it possible to interact with octet streams in the context of things like TCP streams and file system operations.

**Streams** in nodejs means a sequence of data being moved from one point to the other over time. you have a huge data to process, but dont need to wait for all data to be available before start processing.

if the rate data arrives is faster than the rate the process consumes the data, the excess data **need to wait somewhere** for its turn to be processed. if the process is consuming the data faster than it arrives, the few data that arrives earlier **need to wait** for a certain amount of data to arrive before being sent out for processing.

The **waiting area** is athe buffer. A small physical location (usually in the RAM) where data are temporarily gathered,wait and are eventually sent out for processing during streaming.

## notes

- **Blocking vs non-blocking software development** ― blocking executes synchronously and non-blocking asynch-ly.
- `_dirname` ― returns the path of the folder where the current Javascript file resides. tells you the absolute path of the directory containing the currently executing file.
