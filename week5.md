# Week 5 – Performance Monitoring and Baseline Data Collection

## 1. Purpose of Performance Monitoring

From this week onward, system administration and monitoring tasks are performed using a
dedicated administrative user account (`adminuser`) rather than the default user. This
approach follows the principle of least privilege by separating standard user activity
from administrative tasks and requiring explicit privilege elevation via `sudo` only
when necessary.

Using a dedicated administrative account improves accountability and reduces the risk
associated with routine operation under elevated privileges.


The purpose of this week was to monitor and record baseline performance metrics on the
Ubuntu Server. Establishing normal system behaviour under idle conditions provides a
reference point for evaluating system performance during stress testing in later weeks.



## 2. Monitoring Tools Installation

### 2.1 Installed Monitoring Tools

A set of command-line monitoring tools was installed to observe CPU, memory, disk, and
network performance. These tools support both real-time and historical analysis of
system resource usage.

The following tools were installed:
- `htop` for CPU and memory monitoring
- `sysstat` for historical performance statistics
- `iotop` for disk I/O monitoring
- `iftop` for network traffic monitoring



## 3. Baseline System Information

### 3.1 CPU and Kernel Information

CPU and kernel information was collected to document the system architecture and
processing capabilities prior to performance testing.



### 3.2 Memory Baseline

Memory usage was measured while the system was idle to establish a baseline for
comparison during later performance testing.



### 3.3 Disk Usage Baseline

Disk usage statistics were collected to record current storage utilisation and available
capacity on the system.



### 3.4 System Load and Uptime

System uptime and load averages were recorded to confirm that baseline measurements were
taken under minimal system load.



## 4. Real-Time Performance Monitoring

### 4.1 CPU and Memory Monitoring

Real-time monitoring using `htop` showed low CPU and memory utilisation, confirming that
the system was operating under idle conditions during baseline data collection.



### 4.2 Disk I/O Monitoring

Disk I/O activity was monitored using `iotop`, showing minimal read and write operations
during baseline conditions.



### 4.3 Network Activity Monitoring

Network activity was monitored using `iftop`, confirming minimal network traffic while
the system was idle.



## 5. Baseline Performance Summary

Under idle conditions, the Ubuntu Server demonstrated low CPU utilisation, stable memory
usage, negligible disk I/O, and minimal network activity. These baseline measurements
provide a reference point for evaluating system behaviour under stress testing in later
weeks.



## 6. Week 5 Reflection

Week 5 focused on observing and documenting baseline system performance using a range of
monitoring tools. Understanding normal system behaviour is essential before applying
artificial load, as it allows performance degradation and bottlenecks to be accurately
identified.

This week reinforced the importance of proactive monitoring and careful data collection
as part of system performance analysis and capacity planning.

