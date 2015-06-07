# P4 Workshop
At Stanford University, June 4, 2015
[schedule](https://p4workshop2015.sched.org/) 

## Open KeyNotes
Nick McKeown, Stanford

"P4 is a declarative language for expressing how packets are processed by the pipeline
of a network forwarding element such as a switch, NIC, router or network function appliance. It is based upon an abstract forwarding model consisting of a parser and a set of `match+action` table resources, divided between ingress and egress. The parser identifies the headers present in each incoming packet. Each `match+action` table performs a lookup on a subset of header fields and applies the actions corresponding to the first match within each table."

This allows the data plane, the network forwarding behavior, to be programmable declaratively. At the same time, this facilitates the SoC for forwarding network to be developed, such as CPU in general purpose computing, GPU in Graphics, DSP in Signal Processing-dsp. Some research report indicated this special purpose network chip can improve the network bandwidth 50x (3.2Tb/s); which is 50x faster than using CPU.

A logic architecture, Protocal Independent Switch Architecture (PISA), was proposed. 
<<add diagram here>>

## Abstract Forwarding Model 
for P4 spce v1.0, March 3, 2015
[p4 code](https://github.com/p4lang/p4factory)
![Abstract Model](https://www.evernote.com/l/AS5eVDYwUrRMxrr5xBnvzVjGdX3tQR-D2iEB/image.png)

A P4 program contains definitions of the following key components:

* Headers: A header definition describes the sequence and structure of a series of fields. It includes specification of field widths and constraints on field values.

* Parsers: A parser definition specifies how to identify headers and valid header sequences within packets.

* Tables: Match+action tables are the mechanism for performing packet processing. The P4 program defines the fields on which a table may match and the actions it may
execute.

* Actions: P4 supports construction of complex actions from simpler protocol-independent primitives. These complex actions are available within match+action tables.

* Pipeline layout: the layout of tables within the pipeline and the packet flow through the pipeline.

* Control Programs: The control program determines the order of match+action tables that are applied to a packet. A simple imperative program describe the flow of
control between match+action tables.

P4 addresses the configuration of a forwarding element. Once configured, tables may
be populated and packet processing takes place. These po

P4 is essential but not differentiate the service offers.

## Innovation in P4 Stack
Jennifer Rexford

![compiler](https://www.evernote.com/l/AS7oPEqYduFF_4F7nzCo1E08JBRcmmLXL14B/image.png)

* Simple API
* Data-plane policy as function <<- important concept
* Slicing (OvX, multiple tenants, traffic isolation)
* Composition
* Abstract topology, network info base
* Open "as is"
* P4(config, populating)

## Programming Network Datapath
Changhoon Kim

Intuitive abstractions
control flow (match/action)*n

Common industry wide dataplane  programming language,

## P4 Applied to a vSwitch Data Plane
Intel

Converts OvS rules into the underlying data plane
Programmable pipeline underneath OvS

## P4 & Switch Abstraction Interface (SAI) 
Lihua Yuan, Microsoft Azure Networking

SAI Interop Demo at OCP
put control in app-x instead Operating system
Define a SAI-compliant pipeline that can be mapped to a software switch

## Panel on User Perspectives

* Cisco - more critical tech, P4 adds structure, move HW bug to SW (in service upgrade), Questions: keep up with others, what is the data sheet look like, HW has different displines.
* Apple - P4 adds operation efficiency
* Google - switch is one program used on Network, data center, WAN. Operating environment becomes so complicate, solution is to stay in one box. Network needs more adaptive. P4 runs on Google Compute Platform.

Change switch state, switch function is forwarding/traffic engineering behavior.
Latency is critical in data center than in network, more than bandwidth. 

## Split/Evolve P4
Mihai Budiu, Barefoot Networks

why:Too big, need to separate architecture from switch program

Wishlist:
- typing, modularity, error handling, simplicity and clarity

send input to p4-design@p4.org

Use OCaml and Rodin to verify P4 program

## Compiling Network Program
Nate Foster, Cornell

[netkat](http://www.cs.cornell.edu/~jnfoster/papers/frenetic-netkat.pdf)
NetKat - functional
network virtualization
automatic verification
fault tolerance
application Intent
formalize top down (you can use open flow as sub-language)

Integer Linear Programming
TDG table dependency graph

![TDG table dependency graph](https://www.evernote.com/l/AS6UpKl8DXRKULqLaNWvxtqiDxqn7DUdODwB/image.png)

## Notes
[P4: Programming Protocol-Independent Packet Processors](http://www.sigcomm.org/sites/default/files/ccr/papers/2014/July/0000000-0000004.pdf)

### P4 goals: 

1. Reconfigurability in the field: Programmers should be able to change the way switches process packets once they are deployed. 

2. Protocol independence: Switches should not be tied to any specific network protocols. 

3. Target independence: Programmers should be able to describe packetprocessing
functionality independently of the specifics of the underlying hardware.
