# Motivation
## Example of File Sharing System
Bob wants to share his movies to his friends, and also wants to get other movies from their friends.
![[Pasted image 20260313140649.png]]
### Client - Server Architecture
![[Pasted image 20260313140846.png]]
### Peer-to-Peer Architecture
![[Pasted image 20260313140915.png]]
### Cluster Architecture
![[Pasted image 20260313140941.png]]
## Compare
![[Pasted image 20260313141018.png]]

## Challenges
![[Pasted image 20260313141317.png]]
# Concepts and Use-cases
**Before** distributed systems there are parallel computing during 70s and 80s
**Earlier distributed systems** started dominating in the 1990s: The WWW, Airline reservation systems, Banking systems
## Distributed vs Parallel Computing
![[Pasted image 20260313141558.png]]
## Definition
A **distributed system** is a **collection** of **independent computers (nodes)** that **work together, sharing resources** like data or processing power and **appearing** to users **as**
**a single coherent system** .

![[Pasted image 20260313141803.png]]
## Network Computers vs Distributed System
|Aspect|Network Computer|Distributed System|
|---|---|---|
|**Purpose**|Connect independent machines for resource sharing (files, printers).|Multiple machines collaborate as single logical system (e.g., Google search spans 1000s servers invisibly).ecomputertips​|
|**User View**|Sees separate computers; must specify "server IP" or shared folder.|Single interface; "Google.com" hides 1000s servers behind it.tutorialspoint​|
|**Coordination**|Each runs own OS; manual resource access.|Shared OS layer manages resources across nodes automatically.guvi​|
|**Failure Impact**|One machine down? Others work fine.|Designed fault-tolerant; single node failure doesn't crash system.tutorialspoint​|
|**Communication**|File/printer sharing via SMB/NFS.|Message passing (like your chat app sockets) or RPC (RMI).ecomputertips​|
|**Course Relevance**|Assignment #2 (Socket Programming) builds network basics.|Project #7 (Real-time chat) creates distributed system atop sockets.github​|
## Other Scenatios
![[Pasted image 20260313142419.png]]
![[Pasted image 20260313142436.png]]
![[Pasted image 20260313142448.png]]
![[Pasted image 20260313142506.png]]
![[Pasted image 20260313142521.png]]
![[Pasted image 20260313142540.png]]
### Supporting Technology
Toolkit or platform for computer to talk (?)
![[Pasted image 20260313142851.png]]
### Distributed Systems Lead To
- **Concurrency**: Concurrent program execution (accesses to the same resource at the same time)
- **No global clock**: Limits to the accuracy with which the computers in a network can synchronize their clocks. 
- **Independent failures**: Each component of the system can fail independently, leaving the others still running
# Challenges
![[Pasted image 20260313143316.png]]
![[Pasted image 20260313143349.png]]
![[Pasted image 20260313143418.png]]
![[Pasted image 20260313143444.png]]
![[Pasted image 20260313143527.png]]
# Characteristics
![[Pasted image 20260313143603.png]]
# Trends in Distributed Systems
![[Pasted image 20260313143721.png]]
![[Pasted image 20260313143806.png]]
![[Pasted image 20260313143846.png]]
# Summary
Motivation behind Distributed System, interact /w DS all the time, Inherent problems in Centralized Systems. **Defined a distributed system**: 
*"System of several processes, running on different computers, communicating with each other through the network, and are sharing a state or working together to achieve a common goal."*
# Discussion
Q1. Can you differentiate the three systems:
- Centralized systems
- De-centralized systems
- Distributed systems

Q2. What should not we expect in distributed systems when we design them?

Q3. Can you differentiate the two systems below?
- Distributed Computing
- Parallel Computing