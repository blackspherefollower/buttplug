# Architecture


## Implementation Types

The Buttplug Standard can be implemented in different ways. This section covers the terms used throughout this document.


### Libraries

Implementing the standard as a library for a certain programming language allows developers to either build servers on top of the library in that language, or to integrate the library into their applications that also use that language (or FFI/bindings to that language). For instance, the C# implementation of the Buttplug Standard can be used with a WebSocket implementation on top of it to be a server that other applications can talk to. It could also be compiled into a Unity game so that the communication exists only in the executable itself.


### Servers

As mentioned above, servers are a thin layer on top of a library that allow other applications to access hardware managed by the server. For instance, a Web Application may not have the capability to talk to hardware by itself, but can connect with a Buttplug Server implementation via HTTP, WebSockets, or other standardized protocols. Programs like Max/MSP and Pd could communicate with a Buttplug Server implementation via OSC.


### Applications (aka Clients)

Applications, or clients, refer to programs that in some way interact with a server to perform some sort of job for the user. A few ideas for applications:

-   A movie player that sends synchronization commands while playing an encoded video.
-   A music player that syncs sex toys with the BPM of the current track.
-   A video game that somehow involves sex toy interaction

All of these would need to talk to a Buttplug server to establish which devices to use, then communicate with those devices.


## Protocol

The Buttplug Standard defines a message based protocol between a client and a server. Note that the use of client and server here does not explicitly denote network connection. These terms are used as a generic way to denote different communication endpoints.

Client are expected to request information from the server about devices that are connected, and to send information to those devices via the server. Servers will handle device enumeration, connection management, and failure recoveries (for instance, stopping all connected devices on client disconnect).

While serialization formats are not yet standardized, current references implementations of the Standard use JSON for serialization. More information on this is available in the Messages section.


## Stages

Buttplug sessions consist of 3 stages. While these stages need not be discrete, due to the way Buttplug will likely be used, they will usually end up being so. Applications may hide or combine some of the stages depending on requirements.


### Identification

During the identification stage, a client will establish connection with the server, and send over its identifying information. The server may trigger some sort of UI event at this point to ask if the user will allow the client to connect and interact.


### Enumeration

After the client/server connection is set up, device enumeration can begin. The client can ask the server to scan for devices on various busses or media (serial, usb, bluetooth, network, etc), and return a list of devices it can communicate with.


### Consummation

Once devices are found and selected, we can assume the user will begin interacting with connected devices. At this point, the client will mostly be sending and receiving device commands. It can usually (but not always) be assumed that continued enumeration may not be possible due to the context of situations that Buttplug software will be used in.
