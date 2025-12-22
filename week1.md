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
private environment for secure SSH-based administration [3]. This design reflects
industry-standard practice in server and cloud environments, where headless systems
are managed remotely to improve security and resource efficiency.

This architecture provides a secure foundation for implementing SSH hardening,
firewall rules, and performance monitoring in later weeks of the coursework.

## 2. Distribution Selection Justification

### Server Distribution: Ubuntu Server

Ubuntu Server was selected as the server operating system due to its stability,
long-term support (LTS), and strong focus on headless server deployment [1]. LTS releases
receive security updates for up to five years, making them suitable for systems that
require consistent configuration and maintenance over time.[1]

Ubuntu Server installs without a graphical interface by default, reducing resource
consumption and minimising the system attack surface [1]. This aligns with the coursework
focus on security hardening, performance evaluation, and command-line administration.[1]

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
user-friendly desktop environment, and compatibility with Ubuntu-based systems [2].
As Linux Mint uses the same package management system (`apt`), it simplifies remote
administration, scripting, and monitoring tasks performed via SSH.

## 3. Workstation Configuration Decision

<img width="1651" height="868" alt="Screenshot 2025-12-20 010646" src="https://github.com/user-attachments/assets/1cbea351-f24b-42b1-b570-a6cce50cc611" />

For this coursework, a Linux desktop virtual machine running Linux Mint was selected as
the workstation system. This workstation provides a dedicated environment for remote
administration, monitoring, and documentation tasks.

Using a Linux-based workstation ensures native support for SSH, command-line tools, and
scripting utilities required throughout the coursework. Linux Mint offers a stable and
user-friendly desktop environment, allowing focus on server administration rather than
workstation configuration complexity.

Separating the workstation from the server system reflects industry-standard practice,
where administrators manage headless servers remotely rather than directly interacting
with the server console.

## 4. Network Configuration Documentation

<img width="626" height="474" alt="Screenshot 2025-12-20 011933" src="https://github.com/user-attachments/assets/84261600-1806-4584-93ec-a58479abed71" />
<img width="634" height="470" alt="Screenshot 2025-12-20 011924" src="https://github.com/user-attachments/assets/15d0c1b3-c9b3-42a2-a0df-8e89d0cf0234" />

<img width="628" height="478" alt="Screenshot 2025-12-20 012034" src="https://github.com/user-attachments/assets/4ec39ca4-fa88-4ca0-8506-9344e4e72ce3" />
<img width="628" height="470" alt="Screenshot 2025-12-20 012020" src="https://github.com/user-attachments/assets/911def0e-29c9-4f78-9de6-9112cff22a61" />

Both the Linux Mint workstation and the Ubuntu Server were configured with two network
adapters. The first adapter uses NAT to provide internet access for system updates and
package installation [3]. The second adapter uses a VirtualBox host-only network, creating a
private and isolated network between the two virtual machines [3].

This configuration allows secure communication between the workstation and server while
ensuring all administration and testing remain contained within the virtual environment.

<img width="1304" height="681" alt="Screenshot 2025-12-20 013735" src="https://github.com/user-attachments/assets/a9cfb0da-4d93-44ba-a333-86d98159848c" />

The `ip addr` command was used on the Linux Mint workstation to display network
interfaces and assigned IP addresses [4]. The output shows two active interfaces: one
providing internet access via NAT and a second interface assigned a private IP address
by the VirtualBox host-only network.

The private IP address confirms correct network configuration and enables direct,
isolated communication with the Ubuntu Server for remote administration tasks.

<img width="1339" height="705" alt="Screenshot 2025-12-20 014345" src="https://github.com/user-attachments/assets/37fd643d-538a-44fe-ba36-751e571eff24" />

The `ip addr` command was executed on the Ubuntu Server to display network interfaces
and IP configuration. The output shows two active interfaces: one using NAT to provide
internet access and a second interface assigned a private IP address by the VirtualBox
host-only network.

The server was assigned a private IP address within the same subnet as the Linux Mint
workstation, enabling secure and isolated communication for remote administration tasks.

## 5. Server System Specifications

<img width="1102" height="40" alt="Screenshot 2025-12-20 014723" src="https://github.com/user-attachments/assets/8debdad3-6856-43bc-9c47-5255d481a1a2" />

The `uname -a` command was used to display kernel and system information for the Ubuntu
Server. This output confirms the Linux kernel version, system architecture, and Ubuntu
kernel build currently in use, providing a baseline reference for the server environment.

<img width="670" height="71" alt="Screenshot 2025-12-20 014839" src="https://github.com/user-attachments/assets/6673ce1c-f5c8-4cd7-a62f-316466f3c371" />

The `free -h` command was used to display system memory usage in a human-readable format.
The output shows total, used, and available memory on the Ubuntu Server, providing a
baseline overview of system capacity prior to performance testing and monitoring.

<img width="426" height="121" alt="Screenshot 2025-12-20 015015" src="https://github.com/user-attachments/assets/19755ef4-9cd2-440c-897f-15c0fc1b2b17" />

The `df -h` command was used to display disk usage across mounted filesystems. The output
shows available and used storage space on the Ubuntu Server, providing a baseline
reference for disk capacity prior to application deployment and testing.

<img width="330" height="111" alt="Screenshot 2025-12-20 015112" src="https://github.com/user-attachments/assets/19c64cd6-fac5-4c3e-9d5e-eb25768e3b0a" />

The `lsb_release -a` command was used to confirm the Linux distribution and version
running on the server. The output verifies that the system is running Ubuntu Server
24.04 LTS, documenting the exact operating system release used for this coursework.

### Week 1 Reflection

This week focused on planning and documenting the system architecture and baseline
configuration for the coursework. Establishing a clear separation between the
workstation and server, along with a secure network design, provides a strong
foundation for implementing security controls and monitoring in later weeks.

## References

[1]
“Introduction | Server documentation,” Ubuntu, 2024. https://ubuntu.com/server/docs

‌[2]
“Documentation - Linux Mint,” linuxmint.com. https://linuxmint.com/documentation.php

‌[3]
“Chapter 6. Virtual Networking,” Virtualbox.org, 2000. https://www.virtualbox.org/manual/ch06.html

‌[4]
“Linux man pages online,” man7.org. https://man7.org/linux/man-pages/index.html
