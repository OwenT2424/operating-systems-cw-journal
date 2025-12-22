# Week 7 – System Evaluation and Optimisation

## 1. System Performance Evaluation

Baseline performance measurements collected in Week 5 showed low CPU utilisation,
stable memory usage, minimal disk I/O, and negligible network traffic under idle
conditions. These measurements provided a reference point for later analysis.

During Week 6 stress testing, the system demonstrated predictable increases in
resource utilisation when subjected to CPU, memory, disk, and network load. CPU
stress resulted in full utilisation across all cores, memory stress increased RAM
usage with minor swap activity, disk stress produced sustained write throughput,
and network stress achieved high data transfer rates.

Despite these increases, the system remained stable and responsive, indicating that
the server configuration is capable of handling moderate to high workloads.

## 2. Security Evaluation

Security controls implemented earlier in the coursework contributed to a hardened
system configuration. SSH access was secured using key-based authentication, root
login was disabled, and password authentication was turned off to reduce the risk
of brute-force attacks.

Firewall rules restricted incoming connections while allowing required services,
and automatic updates ensured that security patches are applied regularly. User
privilege separation through the use of a dedicated administrative account further
reduced risk.

Overall, the system demonstrates a strong security posture appropriate for a
headless server environment.

## 3. Identified Limitations

The server environment is limited by the resources allocated to the virtual machine,
including CPU cores, memory, and disk performance. Under sustained stress, resource
contention could become a bottleneck for more demanding workloads.

Additionally, performance results may differ from those of a physical server due to
virtualisation overhead. Network testing was conducted within a host-only virtual
network, which does not fully represent real-world internet conditions.

## 4. Potential Optimisations

System performance could be improved by allocating additional CPU cores and memory
to the virtual machine or by migrating workloads to a physical or cloud-based server.

Further optimisations may include tuning kernel parameters, implementing monitoring
alerts, and using more advanced performance analysis tools. From a security
perspective, additional measures such as intrusion detection systems and enhanced
logging could be introduced.

## 5. Final Reflection

This coursework provided practical experience across the full lifecycle of server
deployment, from planning and secure configuration to performance monitoring and
evaluation. Establishing baseline measurements before applying stress testing was
critical for understanding how system behaviour changed under load.

The implementation of security controls highlighted the importance of least privilege,
secure authentication, and regular patching in reducing system risk. Performance testing
demonstrated how different system components respond to resource pressure and reinforced
the value of real-time monitoring tools.

Overall, the coursework improved confidence in administering Linux systems, interpreting
performance metrics, and applying security best practices. The skills developed closely
reflect real-world system administration tasks and provide a strong foundation for future
work in server management and performance analysis.

