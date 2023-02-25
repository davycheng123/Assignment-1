# COMP4651 Assignment 01: EC2 Measurement (5 marks)

### Deadline: 23:59, Feb 28, Tuesday

---

### Name: CHENG, Yu Hong
### Student Id: 20689254

### Email: yhchengai@connect.ust.hk

---



## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > SysBench is used. 
    > 
    > The command used for accessing CPU performance was `sysbench cpu --threads=4 --cpu-max-prime=10000 run`.
    > This command asks the CPU to calculate prime number to 10000, which is the maximum allowed, with 4 threads. 
    > The CPU performance is accessed by its speed to see how many events it is capable to handle per second.
    > 
    > The command used for accesing the memory performance was `sysbench memory --threads=4 --memory-total-size=10G --memory-oper=write --memory-scope=global run`.
    > This command asks the computer to test the performance of the memory by writing 10GB of data on it with 4 threads.
    > The memory performance is accessed its writing speed in Mib per second.

2. (1 mark) Run your measurement tool on general purpose `t2.small`, `t3.medium`, and `c3.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **N. Virginia** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance   | Memory performance |
    | ----------- | ----------------- | ------------------ |
    | `t2.small`  | 863.39  event/sec |  483.68 MiB/sec    |
    | `t3.medium` | 1703.04 event/sec |  6074.87 MiB/sec   |
    | `c3.large`  | 1434.46 event/sec |  710.19 MiB/sec    |

    > Region: `N. Virginia`. Use `Ubuntu Server 20.04 LTS (HVM)` as AMI.
    > CPU performance of `t2.small` is significantly lower than the other 2, given that it has fewer vCPU than them. 
    > However, `t3.medium`'s CPU performs better than `c3.large` despite they both have 2 vCPUs.
    > 
    > For the memory, `t2.small` has 2GiB, `c3.large` has 3.75GiB, and `t3.medium` has 4GiB. 
    > Although the memory performance ranking corresponds to the growth of the memory size, it is not linear and `t3.medium` clearly has a much higher memory performance.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t2.small` - ``t2.small`` | 990            |  0.548   |   
    | `t3.medium` - `t3.medium` | 4630           |  0.232   |   
    | `c3.large` - `c3.large`   | 615            |  0.190   |   
    | `t2.small` - `c3.large`   | 616            |  0.418   |
    | `t3.medium` - `c3.large`  | 615            |  0.550   |   
    | `t3.medium` - `t2.small`  | 989            |  0.744   |

    > Region: `N. Virginia`. Use `Ubuntu Server 20.04 LTS (HVM)` as AMI. You should launch **6** instances in total.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 24.8           |  63.331  |
    | N. Virginia - N. Virginia | 4630           |  0.232   |
    | Oregon - Oregon           | 4250           |  0.234   |

    > Region: `N. Virginia`/`Oregon`. Use `Ubuntu Server 20.04 LTS (HVM)` as AMI. All instances are `t3.medium`.
    
3. (1 mark) Is network performance consistent over time? You can do measurements at different times of a day and compare the results. Please give at least 2 possible reasons why network performance is inconsistent.

    > Your answer goes here.

