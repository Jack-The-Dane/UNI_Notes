#multithreading #multicore #multitasking
A thread is the smallest unit of cpu utilizisation. 
Multithreaded process vs single-threaded process:
![[Pasted image 20230915082730.png]]
Multithreading allows for multitasking, so one thread can work on a big task, while another thread continues the main program loop:
![[Pasted image 20230915082950.png]]
This gives better responsiveness, better opportunity for resource sharing and better scalability, as threads can be run on different CPU cores in parallel.

When doing concurrent tasks on a single-core system, the processor has to quickly switch between the tasks, only doing a little bit of the task at a time.
On a multi-core system the threads can be split between the cores.

There are two types of parallelism:
![[Pasted image 20230915083542.png]]

Amdahl's law:
#Amdahl #speedup
$$speedup \leq \frac{1}{S+\frac{(1-S)}{N}}$$
where:
S is the the portion of the application that must be performed serially (can not be split up).
(1-S) is the portion of the application that can be performed in parallel.
N is the number of CPU cores.
This equation describes how much your program can benefit from multitasking.

Challenges of multicore programming:
![[Pasted image 20230915083944.png]]

### Multithreading models
Many to one:
![[Pasted image 20230915084247.png]]
Needs some kind of mapping between the kernel thread and the user threads, done through system calls.
Can be blocked if one user occupies the kernel thread.

One-to-One model:
![[Pasted image 20230915084456.png]]
With more CPU cores, it is possible to have more kernel threads, allowing each user their own kernel thread. This solves the problem of blocking, but is more expensive in core maintenance tasks.

Many-to-Many:
![[Pasted image 20230915084628.png]]
Solves the problem of blocking, as you can just give a user a new thread, if the current one is blocked. Minimizes how many kernel threads are needed.

Two-level model:
![[Pasted image 20230915084800.png]]

# CPU Scheduling
Design objectives, when designing a CPU scheduling algorithm:
![[Pasted image 20230915085409.png]]

Scheduling methods (single core, many processes)
First-come, First-Served (FCFS)
![[Pasted image 20230915085804.png]]
With this method, the average waiting time will vary depending on what order the tasks arrive in. This is called the convoy effect, because all other processes are waiting for the big process to be finished on the CPU core.

Shortest-job-first (SJF):
![[Pasted image 20230915090057.png]]
This method aims to reduce waiting time by executing the shortest jobs first.
This is non-preemptive scheduling.

With preemptive scheduling:
![[Pasted image 20230915090504.png]]
If the tasks dont arrive at the same time, the CPU will stop execution of the current task, if a higher priority task (shorter burst time) arrives. The CPU compares the remaining time of the current task and the time of the incoming task, and switches task if the new task takes less time than the current task has left. This is called preemptive scheduling and Shortest-remaining-time-first. 

This algorithm can be used to predict the CPU burst time of a task:
![[Pasted image 20230915092406.png]]
This equation is used iteratively to predict CPU burst durations. $\alpha$ is often set 0,5.

Round-Robin (RR):
![[Pasted image 20230915092742.png]]
Switches tasks every time a "time slice" has passed. If the time slice towards infinity, this becomes FCFS.
Effect of the time slice on context switches:
![[Pasted image 20230915093315.png]]
A good rule of thumb is that 80% of CPU bursts should be shorter than the time slice, as context switches are very expensive for the CPU.

Priority scheduling:
![[Pasted image 20230915093523.png]]
This method has a problem of the task with the lowest priority may never be executed (Starvation).
Priority scheduling can be combined with round robin, so highest priority is executed first, but tasks with the same priority will be switched between using Round Robin.

Multilevel Queue Scheduling:
![[Pasted image 20230915094159.png]]
Different groups of processes are assigned different priorities.
This scheduling scheme is used in Windows.

Multilevel Feedback Queue Scheduling:
![[Pasted image 20230915094418.png]]
Priority of the task depends on the burst time of the task. Longer times will give lower priority.

Multi-processor scheduling:
![[Pasted image 20230915094716.png]]

Memory stall:
A CPU core will spend a lot of time waiting for memory calls, which gives a lot of idle time for the core. This can be mitigated by using the core for another thread, while it is waiting for the memory in the original thread. This doubles the number of hardware threads you can have per core.
![[Pasted image 20230915095528.png]]

Two levels of scheduling:
![[Pasted image 20230915095731.png]]

Real-time CPU scheduling:
#realtime
![[Pasted image 20230915095832.png]]
![[Pasted image 20230915100236.png]]

Priority-Based Real-Time Scheduling:
![[Pasted image 20230915100508.png]]

Rate-Monotonic Real-Time Scheduling:
![[Pasted image 20230915100647.png]]
The formula for CPU usage at worst case is given by:
$$\text{CPU Usage}_{\text{worst case}} = N \cdot (2^{1 \over N}-1)$$
N is the number of processes.

Earliest-Deadline-First (EDF) Real-Time Scheduling:
![[Pasted image 20230915101528.png]]
