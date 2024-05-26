# Fault Tolerance 

### Q1. What is Fault tolerance ? Explain the failure models of fault tolerance.

- Fault tolerance in distributed systems refers to the ability of a system to continue functioning correctly even in the presence of faults.
- Faults can occur due to hardware failures, software bugs, network issues, or other unexpected problems.
- A fault-tolerant system is designed to detect, isolate, and recover from these faults, ensuring minimal impact on the overall system performance and availability.
- Redundancy: Multiple copies of data and services are maintained across different nodes to ensure that if one node fails, others can take over its responsibilities.
- Failure Detection: Mechanisms are in place to quickly detect failures in nodes, components, or network connections. Common techniques include heartbeats (regular signals sent between nodes) and monitoring tools.

### Failure Models in Distributed Systems

1. **Omission Failures**:
   - **Description**: Omission failures occur when a process or communication channel fails to perform its required actions. This can manifest as a process not sending a message it was supposed to send (send omission) or not receiving a message it was supposed to receive (receive omission).
   - **Examples**:
     - **Process Omission**: A server fails to respond to a client's request.
     - **Channel Omission**: A message sent over a network is lost due to network issues.
 
2. **Arbitrary (Byzantine) Failures**:
   - **Description**: Arbitrary failures, also known as Byzantine failures, involve components behaving erratically or maliciously. They can send incorrect, inconsistent, or misleading information, making them the most challenging type of failure to handle.
   - **Examples**:
     - A node sends different data to different parts of the system.
     - A compromised node behaves maliciously, trying to disrupt the system.
  
3. **Timing Failures**:
   - **Description**: Timing failures occur when components fail to meet specified time constraints in a synchronous distributed system. These failures happen when operations take too long or complete too early relative to their expected timing.
   - **Examples**:
     - A process fails to complete a task within a defined time limit.
     - Network delays cause messages to arrive late, missing their deadlines.
  

4. **Crash Failures**:
   - **Description**: Crash failures occur when a process or node stops functioning altogether and does not recover on its own. Unlike arbitrary failures, crash failures are simpler as the faulty component simply stops.
   - **Examples**:
     - A server crashes and becomes unresponsive due to a hardware fault.
     - A process terminates unexpectedly due to a software bug.

By understanding and addressing the various failure models, distributed systems can be designed to be resilient and maintain high availability and reliability even in the presence of faults

---

### Q2. What is Failure Masking? Explain Failure masking by redundancy ?
- Failure masking is a technique used in distributed systems to hide or "mask" the effects of failures from the users and other parts of the system, ensuring that the system continues to operate correctly despite the presence of faults.
- The goal is to provide a seamless experience, maintaining the system's functionality and reliability even when some components fail.
- It makes the system appear fault-free even when failures occur.

### Failure Masking by Redundancy

One of the primary methods to achieve failure masking is through redundancy. Redundancy involves duplicating critical components or data so that if one part fails, another can take over without disrupting the overall system operation. Here's a detailed explanation of how redundancy helps in failure masking:

#### Types of Redundancy

1. **Data Redundancy**:
   - **Description**: Multiple copies of data are stored in different locations or nodes.
   - **Example**: In distributed databases or file systems, data is replicated across several nodes. If one node fails, the data can still be accessed from other nodes.
   - **Benefit**: Ensures data availability and protects against data loss due to node failures.

2. **Hardware Redundancy**:
   - **Description**: Critical hardware components are duplicated.
   - **Example**: Servers, storage devices, and network components are duplicated in data centers. If a primary server fails, a secondary server can take over.
   - **Benefit**: Increases system reliability by providing backup hardware to take over in case of failures.

3. **Software Redundancy**:
   - **Description**: Software processes or services are replicated.
   - **Example**: Microservices architecture where multiple instances of a service run simultaneously. If one instance fails, other instances handle the load.
   - **Benefit**: Ensures service continuity and load balancing.

4. **Time Redundancy**:
   - **Description**: Operations are repeated over time to ensure success.
   - **Example**: Retransmitting a network packet if an acknowledgment is not received within a certain timeframe.
   - **Benefit**: Overcomes transient faults that might affect operations intermittently.

### Example Scenario: Cloud Storage Systems

Consider a cloud storage service like Google Drive or Amazon S3:

- **Data Redundancy**: Files uploaded to the cloud are replicated across multiple data centers in different geographic locations.
- **Failover Mechanism**: If one data center experiences a failure, another data center with replicated files can serve the users' requests.
- **Load Balancing**: User requests are distributed across multiple servers to ensure no single server is overwhelmed, and redundant servers are available to take over in case of a failure.
- **Error Detection and Correction**: Data integrity checks (e.g., checksums) are performed to detect and correct errors in stored files.

By using redundancy, the cloud storage service masks failures effectively, ensuring that users always have access to their files without experiencing disruptions due to underlying component failures. This provides a seamless and reliable user experience, demonstrating the power of failure masking through redundancy.

---

### Q3. What do you mean by Failure Recovery ? Explain various failure recovery techniques.

- Failure recovery in distributed systems refers to the processes and mechanisms employed to restore a system to a normal operating state after a failure has occurred.
- The goal is to minimize downtime, maintain data integrity, and ensure that the system can continue to function correctly.
- Failure recovery involves detecting the failure, isolating and diagnosing the problem, and then applying the necessary steps to bring the system back to a fully operational state.
- Failure Detection: Identifying when and where a failure has occurred. This often involves monitoring system components for signs of malfunction or using heartbeats and timeouts to detect unresponsive nodes.
- Failure Isolation:  Isolating the faulty component to prevent the failure from propagating and affecting other parts of the system.
- Diagnosis: Determining the cause and nature of the failure. This helps in applying the appropriate recovery strategy.
- Recovery Strategies: Implementing the steps needed to recover from the failure and restore normal operations. This may involve restarting services, switching to backup systems, or restoring data from backups.


- Classification of Failures
Failures in a computer system can be classified as follows :
1. Process failure
2. System failure
3. Secondary storage failure
4. Communication medium failure. 

### Various Failure Recovery Techniques

1. **Checkpointing and Rollback Recovery**:
   - **Checkpointing**: The system periodically saves its state (checkpoints) to stable storage. If a failure occurs, the system can roll back to the last saved state.
   - **Rollback Recovery**: After a failure, the system reverts to the most recent checkpoint and resumes operation from there, re-executing any operations that occurred after the checkpoint.
   - **Example**: A database system that periodically saves transaction logs and can revert to the last consistent state in case of a crash.

2. **Replication-Based Recovery**:
   - **Data Replication**: Data is replicated across multiple nodes or locations. If one node fails, another node with the replicated data can take over.
   - **Service Replication**: Critical services are duplicated across multiple servers. If one server fails, the service can continue on another server.
   - **Example**: Distributed file systems like HDFS (Hadoop Distributed File System) replicate data blocks across multiple nodes to ensure data availability.


3. **Data Versioning**:
   - **Mechanism**: Multiple versions of data are maintained. In case of a failure, the system can revert to a previous version.
   - **Example**: Version control systems like Git maintain a history of changes, allowing rollback to any previous state.


4. **Message Logging**:
   - **Mechanism**: Message logging involves recording all the messages exchanged between components. In case of a failure, the system can replay the logged messages to restore the state of the failed component.
   - **Types**:
     - **Pessimistic Logging**: Logs messages before they are processed
     - **Optimistic Logging**: Logs messages after processing
   - **Example**: A distributed system logs all inter-process communications. If a node fails, the system replays the logged messages to restore the node's state and ensure continuity.


By combining these recovery techniques, the cloud-hosted web application can achieve high availability, reliability, and resilience, ensuring minimal disruption to users even in the face of component failures.

---

### Q4. Define the terms of group communication  :  Atomic multicast and Distributed Commit OR Describe How reliable group communication achieved in DS.

Group communication involves communication among multiple processes or nodes in a distributed system, often organized into groups or multicast groups. Two important terms in group communication are "Atomic multicast" and "Distributed Commit."

### Atomic Multicast

**Atomic multicast** is a communication primitive in distributed systems that ensures the delivery of messages to multiple recipients in such a way that either all recipients receive the message or none of them receive it. In other words, atomic multicast guarantees atomicity across multiple receivers.

#### Key Characteristics of Atomic Multicast:

1. **Reliable Delivery**: Atomic multicast guarantees that either all group members receive the multicast message or none of them receive it.
2. **Total Order**: Messages delivered by atomic multicast are delivered to all group members in the same order.
3. **Message Integrity**: Atomic multicast ensures that messages are not duplicated or lost in transit.
4. **Group Membership**: It operates within the context of a multicast group, where all members of the group receive the message.

#### Example Use Cases:

- Distributed databases: Ensuring that all replicas of a data item are updated atomically.
- Distributed file systems: Coordinating updates to metadata across multiple servers.
- Replicated state machines: Ensuring that all replicas execute commands in the same order.

### Distributed Commit

**Distributed Commit** refers to the process of coordinating and ensuring the atomic commit of a transaction across multiple nodes or participants in a distributed system. In a distributed transaction, a commit operation should either be applied to all involved nodes (commit) or none of them (abort), ensuring consistency across the system.

#### Key Characteristics of Distributed Commit:

1. **Atomicity**: Distributed commit ensures that all nodes agree to commit or abort a transaction atomically.
2. **Consistency**: If a transaction commits, all changes made by the transaction are reflected in the system. If it aborts, no changes are applied.
3. **Isolation**: Transactions are executed independently of each other, and their effects are isolated until they are committed.
4. **Durability**: Once a transaction commits, its effects are durable and persist even in the face of failures.

#### Example Use Cases:

- Banking systems: Ensuring that a fund transfer transaction updates both the sender's and receiver's accounts atomically.
- E-commerce platforms: Coordinating a purchase transaction that involves deducting inventory from stock and updating customer records.
- Distributed databases: Committing changes made by a transaction across multiple database nodes in a cluster.

Both atomic multicast and distributed commit are fundamental concepts in distributed systems that enable coordination and consistency among distributed processes or nodes. They play crucial roles in ensuring the correctness, reliability, and integrity of distributed applications and services.

---

### Q5. Explain Reliable Client Server Communication in terms of Point-to-Point Communication OR Explain how reliable client server communication can be achieved

### Reliable Client-Server Communication in Terms of Point-to-Point Communication

Reliable client-server communication ensures that messages exchanged between a client and a server are delivered accurately, in order, and without loss or duplication. This is crucial for maintaining data integrity and consistency in distributed systems. Point-to-point communication refers to direct communication between two endpoints (client and server), often using a protocol like TCP to provide reliability.

Here are key aspects and techniques to achieve reliable client-server communication:

1. **Acknowledgments and Timeouts**:
   - **Mechanism**: The sender (client or server) transmits a message and waits for an acknowledgment (ACK) from the receiver. If the ACK is not received within a specified timeout period, the sender retransmits the message.
   - **Example**: TCP uses ACKs and timeouts to ensure reliable delivery of packets. If an ACK for a packet is not received, TCP retransmits the packet.

2. **Retransmissions**:
   - **Mechanism**: If a message or packet is lost or corrupted during transmission, the sender retransmits it. This is usually triggered by the absence of an ACK within the timeout period.
   - **Example**: TCP automatically handles retransmissions of lost packets to ensure reliable communication.

3. **Sequence Numbers**:
   - **Mechanism**: Messages are assigned sequence numbers, allowing the receiver to detect lost, duplicated, or out-of-order messages. The receiver can use these numbers to reorder messages and discard duplicates.
   - **Example**: TCP uses sequence numbers to keep track of the order of packets. This helps in reordering packets that arrive out of sequence and in detecting duplicates.

4. **Error Detection and Correction**:
   - **Mechanism**: Messages include error-detecting codes (e.g., checksums, CRC) that allow the receiver to detect corruption. If corruption is detected, the receiver requests a retransmission.
   - **Example**: TCP includes a checksum in each segment to detect errors. If a segment's checksum does not match, the segment is discarded, and the sender is requested to retransmit it.

5. **Flow Control**:
   - **Mechanism**: Ensures that the sender does not overwhelm the receiver with too many messages at once. Flow control mechanisms regulate the rate of data transmission based on the receiver's capacity.
   - **Example**: TCP uses a sliding window protocol to manage flow control, adjusting the rate of data transmission based on the receiver's buffer capacity.

6. **Congestion Control**:
   - **Mechanism**: Prevents network congestion by controlling the rate of data transmission based on network conditions. Congestion control algorithms adjust the transmission rate to avoid overloading the network.
   - **Example**: TCP uses algorithms like Slow Start, Congestion Avoidance, and Fast Retransmit to manage congestion control.

7. **Persistent Connections**:
   - **Mechanism**: Keeping a connection open for multiple requests and responses between the client and server. This reduces the overhead of establishing and tearing down connections for each communication.
   - **Example**: HTTP/1.1 uses persistent connections to allow multiple HTTP requests and responses to be sent over a single TCP connection.

### Summary

Reliable client-server communication in point-to-point communication ensures that messages are delivered accurately and in order through mechanisms like acknowledgments, retransmissions, sequence numbers, error detection and correction, flow control, and congestion control. TCP (Transmission Control Protocol) is the most common protocol providing these reliability features, making it a foundational technology for reliable communication in distributed systems.


---

### Q6. What is RPC ? Explain RPC Semantics in the presence of failure.


- Remote Procedure Call (RPC) is a protocol that allows a program to execute a procedure (subroutine) on a remote server as if it were a local call.
- This abstraction simplifies the development of distributed systems by allowing developers to write code that calls remote services using the same syntax and semantics as local function calls.
- RPC hides the complexities of the network communication.
- RPC uses stubs (client and server) to facilitate communication. The client stub acts as a proxy for the remote procedure, while the server stub unpacks the request and invokes the procedure.


### RPC Semantics in the Presence of Failures

Failures are a significant concern in distributed systems, and RPC systems must handle various types of failures to ensure robustness. The main types of failures include:

1. **Client Failures**: The client crashes before or after making an RPC call.
2. **Server Failures**: The server crashes before processing the call, during processing, or after processing but before sending the response.
3. **Network Failures**: Messages can be lost, delayed, or duplicated due to network issues.

To handle these failures, RPC semantics define different levels of guarantees regarding the execution of remote procedures. These semantics include:

#### 1. **Exactly Once Semantics**
- **Definition**: The RPC guarantees that the remote procedure is executed exactly once, regardless of failures.

#### 2. **At Most Once Semantics**
- **Definition**: The RPC guarantees that the remote procedure is executed at most once. It might not be executed if a failure occurs before execution.

#### 3. **At Least Once Semantics**
- **Definition**: The RPC guarantees that the remote procedure is executed at least once, but it may be executed more than once if failures occur.

#### 4. **Best Effort Semantics**
- **Definition**: The RPC makes no guarantees about the execution of the remote procedure. It will try to execute the procedure but does not handle failures.

### Handling Failures in RPC

1. **Client-side Timeouts and Retries**: The client waits for a response for a certain period (timeout). If the response is not received
2. **Server-side State Management**: The server maintains a log of requests and their statuses to detect and handle duplicate requests

In summary, RPC is a powerful abstraction for distributed systems, enabling seamless remote procedure execution. Handling failures in RPC involves ensuring reliable communication through mechanisms like retries, unique request identifiers, state management, and designing idempotent operations. The choice of RPC semantics (exactly once, at most once, at least once, or best effort) depends on the application requirements and the nature of the remote procedures.

---

### Q7.  What is process resilience? Describe how process resilience can be achieved.
(process resilience technique?)

- Process resilience in a distributed system refers to the ability of the system to continue operating properly even in the presence of failures of one or more of its components.
- This involves ensuring that the system can handle hardware failures, software bugs, network issues, and other disruptions without significant degradation in performance or availability. Achieving process resilience is crucial for maintaining reliability and availability in distributed systems.
- The more resilient the systems, the more available it is to serve users. 

Here are several strategies to achieve process resilience in distributed systems:

### 1. **Redundancy**
   - **Replication**: By creating multiple copies of data or services across different nodes, the system can continue to function even if some nodes fail. Common replication techniques include master-slave replication, multi-master replication, and quorum-based replication.

### 2. **Failover Mechanisms**
   - **Automatic Failover**: When a failure is detected, the system automatically switches to a backup component without requiring manual intervention. This is often used in conjunction with replication.

### 4. **Fault Detection**
   - **Heartbeat Mechanisms**: Regularly checking the health of components by sending periodic signals. If a component does not respond within a certain timeframe, it is assumed to be failed.

### 5. **Monitoring and Alerting**
   - **Real-time Monitoring**: Continuously monitoring the health and performance of the system components to detect issues early.
   - **Alerting**: Setting up alerts to notify administrators of potential issues before they lead to significant outages.

### 6. **Load Balancers**
   - **Load Balancers**: Distributing workloads across multiple nodes so that if one node fails, the load balancer can redirect traffic to the remaining healthy nodes.

### 7. **Testing - Chaos Engineering**
   - **Simulating Failures**: Intentionally introducing failures into the system to test its resilience and identify weaknesses. This can be done using tools like Chaos Monkey.

### 8. **Backups and Disaster Recovery Plans**
   - **Regular Backups**: Taking regular backups of data and system states to ensure that recovery is possible in case of major failures.
   - **Disaster Recovery Planning**: Developing and testing plans to recover from catastrophic failures, including data center outages.

By implementing these strategies, distributed systems can achieve high levels of resilience, ensuring that they remain operational and reliable even in the face of various types of failures.

---


### Q8. Explain how consensus achieved in faulty systems.(*less chances)
Achieving consensus in faulty systems, particularly in distributed systems where components can fail or behave unpredictably, is a critical challenge. Consensus algorithms are designed to ensure that all non-faulty components in a distributed system agree on a common decision, even in the presence of failures. Here’s an explanation of how consensus can be achieved in such environments, along with a discussion of key algorithms used for this purpose:

**Consensus in Faulty Systems**

Consensus in faulty systems ensures all non-faulty components in a distributed system agree on a common decision, even when some components fail. Key features include:

1. **Agreement**: All non-faulty nodes must agree on the same value.
2. **Validity**: If all non-faulty nodes propose the same value, they must agree on that value.
3. **Termination**: All non-faulty nodes must eventually reach a decision.

**Key Consensus Algorithms**:

1. **Paxos**:
   - Designed for crash failures.
   - Uses proposers, acceptors, and learners.
   - Achieves consensus through prepare, promise, accept, and accepted phases.

2. **Raft**:
   - Simplifies consensus with leader-based approach.
   - Handles crash failures.
   - Consists of leader election and log replication.

3. **Practical Byzantine Fault Tolerance (PBFT)**:
   - Handles arbitrary (Byzantine) failures.
   - Involves pre-prepare, prepare, and commit phases.

Consensus algorithms ensure system reliability and consistency despite failures by using majority quorums, message authentication, and redundancy.

---