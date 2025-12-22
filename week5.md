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

The following tools were installed:
- `htop` for CPU and memory monitoring
- `sysstat` for historical performance statistics
- `iotop` for disk I/O monitoring
- `iftop` for network traffic monitoring

<img width="435" height="82" alt="Screenshot 2025-12-22 061804" src="https://github.com/user-attachments/assets/fb800ae6-ad0f-4435-9d79-9d8790fc8cde" />
<img width="669" height="67" alt="Screenshot 2025-12-22 061853" src="https://github.com/user-attachments/assets/a790bafa-18ed-4e96-bd1c-437a417e2083" />

System monitoring tools were installed and verified on the Ubuntu Server to support
real-time and historical analysis of CPU, memory, disk I/O, and network performance.
These tools will be used to establish baseline system metrics prior to stress testing.

## 3. Baseline System Information

### 3.1 CPU and Kernel Information

<img width="811" height="760" alt="Screenshot 2025-12-22 062615" src="https://github.com/user-attachments/assets/dd5d5f54-7f85-4e4e-982c-299085878a2f" />

CPU and kernel information was collected to document the system architecture and
processing capabilities under idle conditions. This establishes a baseline for
evaluating performance during later stress testing.

### 3.2 Memory Baseline

<img width="818" height="83" alt="Screenshot 2025-12-22 062838" src="https://github.com/user-attachments/assets/14482e06-fdaf-41c0-b027-5b94cf2a7bc1" />

Memory usage was measured while the system was idle to establish a baseline for
comparison during later performance testing.

### 3.3 Disk Usage Baseline

<img width="673" height="195" alt="Screenshot 2025-12-22 063455" src="https://github.com/user-attachments/assets/3faef033-2f4a-4c01-b5a7-c8ca9f2f81d4" />

Disk usage statistics were collected to record current storage utilisation and available
capacity on the system under idle conditions.

### 3.4 System Load and Uptime

<img width="613" height="41" alt="Screenshot 2025-12-22 063747" src="https://github.com/user-attachments/assets/d1e286e9-7412-4f7b-bcab-4c9dc89a62f4" />

System uptime and load averages were recorded to confirm that baseline measurements were
taken while the system was under minimal load.

## 4. Real-Time Performance Monitoring

### 4.1 CPU and Memory Monitoring

<img width="1001" height="202" alt="Screenshot 2025-12-22 064233" src="https://github.com/user-attachments/assets/e8a95c15-4d1f-4cc0-bcbb-89c8ed2ba88b" />

Real-time monitoring using htop showed low CPU and memory utilisation, confirming that
the system was operating under idle conditions.

### 4.2 Disk I/O Monitoring

<img width="735" height="44" alt="Screenshot 2025-12-22 064600" src="https://github.com/user-attachments/assets/f4d8db2a-803c-4d44-ac00-69c8be4873a7" />

Disk I/O activity was monitored using iotop, showing no significant read or write
operations during idle conditions.

### 4.3 Network Activity Monitoring

<img width="983" height="438" alt="Screenshot 2025-12-22 065032" src="https://github.com/user-attachments/assets/b88ec0c2-b94c-41fd-b3aa-1da78a7d0a7a" />

Network traffic was monitored using iftop, confirming minimal network activity while the
system was idle.

## 5. Baseline Performance Summary

Under idle conditions, the Ubuntu Server demonstrated low CPU utilisation, stable memory
usage, negligible disk I/O, and minimal network activity. These measurements establish a
baseline reference for evaluating system behaviour during stress testing in later weeks.

## 6. Week 5 Reflection

Week 5 focused on collecting baseline performance data using a range of monitoring
tools. Observing system behaviour under idle conditions provided insight into normal
resource utilisation and established a reference point for future performance analysis.

This week highlighted the importance of baseline measurement as a foundation for
identifying performance bottlenecks and understanding the impact of system load during
stress testing.

