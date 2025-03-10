#deadlocks #deadlock
A deadlock situation can arise if the following four conditions hold
simultaneously in a system:
**Mutual exclusion:** At least one resource must be held in a
nonsharable mode; that is, only one thread at a time can use the
resource. If another thread requests that resource, the requesting
thread must be delayed until the resource has been released.
**Hold and wait:** a thread holds at least one resource while waiting
for additional resources held by other threads.
**No preemption:** a resource is only released voluntarily by the
thread that holds it when it has completed its task.
**Circular wait:** if there exists a set {T0, T1,…, Tn} of waiting threads
such that T0 waits for a resource held by T1, T1 waits for a resource
held by T2,…, Tn – 1 waits for a resource held by Tn and Tn waiting
for a resource held by T0.

## Characterization (Resource allocation graphs)
![[Pasted image 20230929084153.png]]
![[Pasted image 20230929084219.png]]
![[Pasted image 20230929084244.png]]
![[Pasted image 20230929084305.png]]

**Summary**
If a graph does NOT contain cycles → No deadlock
If a graph contains cycles → possibly cause deadlock
• But ONLY if there is one instance per. resource type
• If there are several instances per. Resource type, there is a risk

## Strategies for managing deadlocks

• I**gnore the problem and pretend that it never occurred…**
e.g.: Unix, Linux, Windows and more… It is then up to kernel and
application developers to write programs that handle deadlocks
(typically using approaches in the second solution)
• **Use a protocol to make sure deadlock never occurs…**
i.e., deadlock prevention and avoidance
• **Allow deadlock to occur and then detect it and recover
afterwards…** i.e., deadlock detection and recovery
e.g.: databases
## Prevention
To prevent the occurence of a deadlock, you simply need to make sure that one of the four previously mentioned conditions can not occur.
### Mutual Exclusion
If we want to break this condition. Then all resources must be
shareable …
It is unrealistic to think that such a system exists…
E.g.: mutex, semaphore, CPU time, etc.

### Hold and Wait
A thread can only start program execution when all the resources it
needs to perform its work can be allocated.
E.g. retrieve data from DVD → save it in a file → read-only file → print
Protocol 1:
allocate DVD, file, printer → perform work→ release resources
protocol 2:
allocate DVD, file → copy → release resources
allocate file → sort → release resources
allocate file, printer → print → release resources
… Poor utilization of resources and possibility of starvation

### No Preemption
A thread that holds resources and requests another resource that cannot
be immediately allocated to it, must implicitly release (devote) all its
allocated resources.
**Alternative:**
A thread that holds resources and requests new resources.
• if they are available, they are taken.
• if they are allocated to a waiting thread, they are taken.
• if they are not available and allocated to a running thread,
the thread has to wait, and all the allocated resources are
preempted
A thread can only continue once it has received all the resources it has
been deprived of (preempted), as well as those it lacked.
… Is often used in connection with resources whose state can be easily saved.

### Circular Wait
Each resource type in the system is assigned a unique integer number,
which allows us to compare two resources and to determine whether
one precedes another in our ordering.
the rule is that all threads only request resources in ascending number
order.
e.g.
R1→R3→R27→R33
if:
R1→R3→R27→R33→ next is R5. Release R27 and R33 and start over…
R1→R3→R5→R27→R33
… There is no guarantee. It requires the threads to comply with the rule
## Avoidance
This strategy requires that the system receive some additional
information about the threads before they are executed.
• The simplest and most useful method is that the thread tells how
many resources (maximum) of each type it may need to use in its
lifetime. Given this a priori information, it is possible to construct
an algorithm that ensures that the system will never enter a
deadlocked state.
• A deadlock-avoidance algorithm dynamically examines the
resource-allocation state to ensure that a circular-wait condition
can never exist.
• The resource-allocation state is defined by the number of
available and allocated resources and the maximum demands of
the threads.

### Safe states
A state is safe if the system can allocate resources to each thread (up to its
maximum) in some order and still avoid a deadlock.
A system is in a safe state only if there exists a safe sequence. A sequence of
threads <T1, T2, …, Tn> is a safe sequence for the current allocation state if,
for each Ti, the resource requests that Ti can still make can be satisfied by
the currently available resources plus the resources held by all Tj, with j < i.
A safe state is not a deadlocked state. Conversely, a deadlocked state is an
unsafe state. However, not all unsafe states are deadlocks. An unsafe state
may lead to a deadlock.
![[Pasted image 20230929092247.png]]
#### Example of safe sequence
Displays three threads using a particular resource with 12 available instances
![[Pasted image 20230929092514.png]]
If there is an order in which the threads can be allocated resources
up to their maximum needs, and release them after use.
Then the system is in safe state because there is a safe sequence.
Here, the safe sequence is: <T1,T0,T2>
If T2 was allocated another instance of the resource (i.e., 3), then a
safe sequence would no longer exist. T1 would be able to get its 2
instances and then release 4 available instances, but neither T0 nor
T2 can be allocated up to their maximum needs of 5 + 5 and 3 + 6
instances, respectively!

### Resource Allocation Graph
In addition to the request and assignment edges in a standard resource-
allocation graph, we introduce a new type of edge, called a claim edge. A
claim edge Ti → Rj indicates that thread Ti may request resource Rj at some
time in the future.
This edge resembles a request edge in direction but is represented in the
graph by a dashed line.
When thread Ti requests resource Rj, the claim edge Ti → Rj is converted to
a request edge.
Similarly, when a resource Rj is released by Ti, the assignment edge Rj → Ti
is reconverted to a claim edge Ti → Rj.
Note that the resources must be claimed a priori in the system. That is,
before thread Ti starts executing, all its claim edges must already appear in
the resource-allocation graph.
![[Pasted image 20230929093511.png]]
Because If T2 requests R2 and gets it allocated to it, this action will create a cycle in the graph. Then we end up in unsafe state!
![[Pasted image 20230929093700.png]]
### Banker's algorithm
We will not go into depth with Banker’s algorithm, but only emphasize
the following points:
▪ A new thread that enters the system must state its maximum needs
for the different types of resources. These needs must not exceed
the total number of different types of resources.
▪ When a thread requests a set of resources, then investigate the
system about if this allocation will leave the system in a safe state.
	o if so, then assign the set of resources to the thread.
	o if no, then the thread has to wait…

#### Example
![[Pasted image 20230929093953.png]]
![[Pasted image 20230929093919.png]]
![[Pasted image 20230929094406.png]]

## Detection
![[Pasted image 20230929095522.png]]
![[Pasted image 20230929095547.png]]
![[Pasted image 20230929095724.png]]

## Recovery
![[Pasted image 20230929100031.png]]
Starvation can happen if a certain process is always chosen to be terminated, because it has low priority. This can be avoided by giving processes higher priority, if they are terminated multiple times.
![[Pasted image 20230929100101.png]]
