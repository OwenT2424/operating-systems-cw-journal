# Week 1 – System Planning & Distribution Selection

## 1. System Architecture Overview

<img width="510" height="258" alt="system architecture design" src="https://github.com/user-attachments/assets/9284904c-f3f2-4ee2-bb09-53aa9e33fc43" />

System architecture diagram showing the Linux Mint workstation used for
remote administration and monitoring, and the Ubuntu Server running headless within an
isolated VirtualBox host-only network. All server administration is performed via SSH
(port 22).

This coursework uses a dual-system architecture consisting of a Linux Mint desktop
workstation and an Ubuntu Server running headless without a graphical interface. The
workstation is used for system administration and monitoring, while the server hosts
test applications and performance monitoring targets.

Both systems are connected using a VirtualBox host-only network, providing an isolated
private environment for secure SSH-based administration. This design reflects
industry-standard practice in server and cloud environments, where headless systems
are managed remotely to improve security and resource efficiency.
