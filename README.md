[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Zhang Hongyu
### Student Id: 21109031
### Email: hzhangfa@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

     `Answer:`

    > Toole : Phoronix Test Suite.
    
    > Parameter Explanation: 
    7zip benchmark is set to evaluate how efficiently the CPU can compress data. The values obtained from measurement results represent CPU performance.
    The ramspeed test measures the memory bandwidth and latency. The values obtained from measurement results represent how quickly the system can read and write data to memory. Therefore, the values mean Memory Performance.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |     3080 MIPS          |         10445.03 MB/s           |
    | `t2.medium`  |         5844 MIPS        |          18818.77 MB/s          |
    | `c5d.large` |        4919 MIPS         |         13752.95 MB/s           |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.
    
     `Answer:`

    >（1）CPU Performance:
    The CPU performance of t2.micro is 3080 MIPS. The t2.micro instance type has 1 virtual CPU (vCPU).
    The CPU performance of t2.medium is 5844 MIPS, nearly double that of t2.micro, indicating a significant improvement in CPU performance as the instance type is upgraded. And the t2.medium instance type has 2 virtual CPU (vCPU) and has 2 cores with 1 thread each.
    The CPU performance of c5d.large is 4919 MIPS, which, although it has fewer vCPUs than t2.medium, still shows good performance due to being a compute-optimized instance. And the c5d.large instance type has 2 virtual CPU (vCPU) and has 1 core with 2 threads. 
    
    >（2）Memory Performance:
    The memory performance of t2.micro is 10445.03 MB/s. The t2.micro instance type has 1 GiB of memory.
    The memory performance of t2.medium is 18818.77 MB/s, almost double that of t2.micro, demonstrating a significant improvement in memory performance as the instance type is upgraded. The t2.medium instance type has 4 GiB of memory.
    The memory performance of c5d.large is 13752.95 MB/s, which is lower than t2.medium but still higher than t2.micro. The c5d.large instance type has 4 GiB of memory.

    > The performance of EC2 instances does indeed increase correspondingly with the increase in the number of vCPUs and memory resources. t2.medium shows a notable performance enhancement, while c5d.large, although slightly lower in CPU and Memory performance, still demonstrates good performance. The difference of threads may cause the difference between t2.medium and c5d.large.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |        4220(4.22 Gbits/sec)        |     0.331     |
    | `m5.large` - `m5.large`   |        4850(4.85 Gbits/sec)        |     0.224     |
    | `c5n.large` - `c5n.large` |        9520(9.52 Gbits/sec)        |     0.104     |
    | `t3.medium` - `c5n.large` |        2700(2.70 Gbits/sec)        |     0.760     |
    | `m5.large` - `c5n.large`  |        4870(4.87 Gbits/sec)        |     0.217     |
    | `m5.large` - `t3.medium`  |        2240(2.24 Gbits/sec)        |     0.637     |
    
    (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.
    
     `Answer:`

    > （1）Same Instance Type: The TCP bandwidth is highest for c5n.large instances, followed by m5.large and t3.medium. The RTT is lowest for c5n.large, indicating better network performance.
    >  (2) Different Instance Types: We can see the TCP bandwidth decreases and RTT tends to be higher when comparing different types. 

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |        32.4        |     64.006     |
    | N. Virginia - N. Virginia |        40200(40.2 Gbits/sec)        |     0.022     |
    | Oregon - Oregon           |        4530(4.53 Gbits/sec)        |     0.134     |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
    
     `Answer:`

    > (1) Inter-Region Performance: The network performance is significantly lower. TCP bandwidth is low and RTT is high, indicating that transferring data between regions is less efficient.
    > (2) Intra-Region Performance: Both show much better performance, especially N. Virginia, which has the highest TCP bandwidth and lowest RTT.
