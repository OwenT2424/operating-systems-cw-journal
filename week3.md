# Week 3 – Application Selection for Performance Testing

## 1. Application Selection Overview

This week focuses on selecting applications that represent different workload types
for performance evaluation on the Ubuntu Server. Each application is chosen to stress
specific system resources, allowing operating system behaviour to be analysed under
varying conditions.

The selected applications will be used consistently in later performance testing and
optimisation tasks to ensure meaningful comparison of results.

## 2. Application Selection Matrix

| Workload Type | Application | Justification |
|--------------|------------|---------------|
| CPU-intensive | stress-ng | Used to generate controlled CPU load and observe scheduling behaviour |
| Memory-intensive | stress-ng | Allows allocation and stressing of system memory |
| Disk I/O-intensive | fio | Used to benchmark disk read and write performance |
| Network-intensive | iperf3 | Measures network throughput and latency |
| Server workload | nginx | Represents a typical web server workload |

## 3. Installation Documentation

The following commands will be used to install the selected applications on the Ubuntu
Server via SSH:

```bash
sudo apt update
sudo apt install stress-ng fio iperf3 nginx -y
```

## 4. Expected Resource Profiles

- stress-ng (CPU): High CPU utilisation across available cores with minimal disk usage.
- stress-ng (Memory): Increased memory allocation and potential swap usage under load.
- fio: High disk read/write activity affecting I/O wait times.
- iperf3: Increased network throughput and associated CPU usage during testing.
- nginx: Moderate CPU and memory usage with network and disk activity depending on request load.

## 5. Monitoring Strategy

Performance monitoring will be conducted remotely from the Linux Mint workstation
using SSH-based commands and scripts. Key metrics to be monitored include CPU usage,
memory usage, disk I/O, and network activity.

Standard Linux tools such as top, free, vmstat, iostat, and ifstat will be used to
collect performance data during baseline and load-testing scenarios.

### Week 3 Reflection

Selecting applications that represent different workload types highlighted how
operating system behaviour can vary significantly depending on resource demands.
This planning ensures that later performance testing and optimisation will be
meaningful and comparable across different scenarios.



