Architecture of the `go-i2p` Namespace
======================================

`go-i2p` is organized as a collection of repositories in the same larger organization-level namespace.
It is intentionally broken down into repositories with a narrow scope and re-usable components.
When navigating the namespace, it helps to think about dependencies and how we move from low-level components built to specification to building a real application.
The dependencies most relevant to navigating our code are generally "internal" dependencies, that is, dependencies maintained by us.
Of course, dependencies are defined to meet a set of requirements, so that's how we name them:

 1. Dependencies of building an I2P Router
 2. Dependencies of interacting with the I2P Network
 3. Dependencies of building an I2P Application

Dependencies of building an I2P Router
--------------------------------------

These are components of the I2P router defined by the specification, organized into a standard library of I2P components.
The most fundamental components are involved with cryptography and encoding/dedoding data at various phases for processing by the router.
These components are also valuable "pre-integration" with the I2P router.
If a third-party non-I2P router required a way to modify Noise for obfuscation-related purposes, then go-i2p/noise would provide them a framework for doing so without tying them to using I2P per se.
From the lowest number of internal dependencies to the highest:

 - github.com/go-i2p/logger - 0 internal dependencies
 - github.com/go-i2p/noise - 0 internal dependencies
 - github.com/go-i2p/crypto - 0 internal dependencies
 - github.com/go-i2p/common - depends on go-i2p/crypto
 - github.com/go-i2p/go-noise - depends on go-i2p/noise and go-i2p/crypto

Dependencies of interacting with the I2P Network
------------------------------------------------

This is where it begins to look like an application, specifically the I2P router itself is built here.
These are components that mostly make sense when you're building an I2P router and not in other places.
They tend to only be useful when integrated with an I2P router and it sits right in the middle of the stack.
At this layer, everything is a "message" of some type or another, being processed by the router.

 - github.com/go-i2p/go-i2p - 5 internal dependencies

This is actually the only relevant repository at this layer.
However, take note of some specific content in this repo:

 - /go-i2p/lib/embedded/README.md - This is the "Embedding Guide" which shows people how to embed the router in another application.
 - /go-i2p/lib/netdb/ISOLATION.md - This is the "NetDB Isolation Documentation" which shows an example of how we secure the router in order to meet unlinkability requirements.

The dependency which is satisfied at this layer is network operation itself.
Technically, at this point, you *could* build an application but it would be difficult.
When communicating over the network with I2CP, you are communicating with messages that don't have any intrinsically relevant data inside them, sort of like you were constructing IP packets and sending them with `SOCK_RAW`.

Dependencies of building an I2P Application
-------------------------------------------

Up here you have components which are used to make application development more straightforward.
Here is also where most of the "action" is happening now.
It helps to think of these repositories as bridging the gap between "meeting the network dependency" and "interfacing with the Go programming language.
Here, libraries may or may not "embed" a router per the guide pointed out above, but they all speak to the router using I2CP to provide interfaces that make sense to applications.

 - github.com/go-i2p/go-sam-go - 0 internal dependencies - does not embed go-i2p/go-i2p
 - github.com/go-i2p/i2pkeys - 1 internal dependency - does not embed go-i2p/go-i2p
 - github.com/go-i2p/go-datagrams - 2 internal dependencies - does not embed go-i2p/go-i2p
 - github.com/go-i2p/go-streaming - 2 internal dependencies - does not embed go-i2p/go-i2p
 - github.com/go-i2p/go-sam-bridge - 9 internal dependencies - does embed go-i2p/go-i2p

Once we're here, we have all the dependencies we need to automate away all the setup process for every application.
What we're getting out of these is specific "protocols" on top of I2CP which map well-known requirements to the I2P environment.
go-i2p/go-datagrams gives us "UDP-like" messaging which is slightly more structured than I2CP messaging, there are 4 types of datagrams in I2P, `RAW`, `DGRAM` a.k.a. legacy repliable. `DGRAM2` a.k.a. modern repliable, and `DGRAM3` which is sort of a hybrid between repliable and raw, which contains the hash of the key of the sender but not the whole destination.
go-i2p/go-streaming provides a more sophisticated, "TCP-like" system which allows for reliable, repliable, replay-resistant messaging between I2P peers.
By combining these in go-i2p/go-sam-bridge we provide a socket-based API for programs to interact with any I2P router on the host, including one "embedded" into the application which starts automatically should no router be available on the host.
go-i2p/go-sam-bridge is itself embeddable, per:

 - /go-sam-bridge/lib/embedding/README.md


go-i2p/go-sam-go is slightly different from the other parts of this section because it *does* depend on an I2P router but it doesn't specifically require our stack, it can work with any I2P router including the Java, C++, and Rust versions.
Finally, we combine `go-i2p/go-sam-bridge` and `go-i2p/go-sam-go` into a single library which automatically ties the lifecycle of the router to the networking requirements of the

 - github.com/go-i2p/onramp - 10 internal dependencies - does embed go-i2p/go-i2p, indirectly, by embedding go-sam-bridge