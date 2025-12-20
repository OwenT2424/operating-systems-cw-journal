# Week 1 – System Planning & Distribution Selection

## 1. System Architecture Overview

<img width="510" height="258" alt="system architecture design" src="https://github.com/user-attachments/assets/9284904c-f3f2-4ee2-bb09-53aa9e33fc43" />

System architecture diagram showing the Linux Mint workstation used for
remote administration and monitoring, and the Ubuntu Server running headless within an
isolated VirtualBox host-only network. All server administration is performed via SSH
(port 22).

This coursework uses a dual-system architecture consisting of a Linux Mint desktop
workstation and an Ubuntu Server running headless without a graphical user interface.
The workstation is used for system administration and monitoring, while the server hosts
test applications and performance monitoring targets.

Both systems are connected using a VirtualBox host-only network, providing an isolated
private environment for secure SSH-based administration. This design reflects
industry-standard practice in server and cloud environments, where headless systems
are managed remotely to improve security and resource efficiency.

This architecture provides a secure foundation for implementing SSH hardening,
firewall rules, and performance monitoring in later weeks of the coursework.

## 2. Distribution Selection Justification

### Server Distribution: Ubuntu Server

Ubuntu Server was selected as the server operating system due to its stability,
long-term support (LTS), and strong focus on headless server deployment. LTS releases
receive security updates for up to five years, making them suitable for systems that
require consistent configuration and maintenance over time.

Ubuntu Server installs without a graphical interface by default, reducing resource
consumption and minimising the system attack surface. This aligns with the coursework
focus on security hardening, performance evaluation, and command-line administration.

In addition, Ubuntu Server is widely used in industry and cloud environments such as
AWS and Microsoft Azure. This makes the skills developed during this coursework directly
transferable to professional system administration and DevOps roles.

**Overall, Ubuntu Server provides a stable and well-documented platform that supports
the implementation of SSH hardening, firewall configuration, monitoring, and security
auditing required in later stages of the coursework.**

### Comparison with Alternative Distributions

Alternative distributions such as CentOS Stream and Arch Linux were considered.
CentOS Stream offers enterprise-level stability but has a steeper learning curve and
slower package update cycle, making it less suitable for rapid experimentation and
learning within an academic environment.

Arch Linux provides maximum system control and very up-to-date packages; however, it
follows a rolling release model, which can introduce instability and increased
maintenance overhead in a server environment.

Debian was also considered due to its reputation for stability; however, Ubuntu Server
provides a more balanced approach by offering newer packages while retaining long-term
support and strong community documentation.

### Workstation Distribution: Linux Mint

Linux Mint was selected as the workstation operating system due to its stability,
user-friendly desktop environment, and compatibility with Ubuntu-based systems.
As Linux Mint uses the same package management system (`apt`), it simplifies remote
administration, scripting, and monitoring tasks performed via SSH.

## 3. Workstation Configuration Decision

<img width="1651" height="868" alt="Screenshot 2025-12-20 010646" src="https://github.com/user-attachments/assets/1cbea351-f24b-42b1-b570-a6cce50cc611" />

Linux Mint desktop workstation running inside VirtualBox. This system is
used as the administrative workstation for SSH access, monitoring, scripting, and
documentation throughout the coursework.

For this coursework, Option A was selected: a Linux desktop virtual machine running
Linux Mint. This workstation provides a dedicated environment for remote administration,
monitoring, and documentation tasks.

