# Week 7 – Security Audit and System Evaluation

## 1. Introduction and Audit Scope

This phase focuses on conducting a security audit and evaluating the overall system
configuration of the Ubuntu Server. The audit assesses infrastructure security, network
exposure, access control mechanisms, running services, and remaining security risks.

## 2. Infrastructure Security Assessment (Lynis)

### 2.1 Initial Lynis Scan (Pre-Remediation)

<img width="640" height="625" alt="Screenshot 2025-12-22 080849" src="https://github.com/user-attachments/assets/f253339c-3d20-48f2-bd40-fb07ef9e9fd6" />

An initial security audit was conducted using Lynis to assess the baseline security posture
of the Ubuntu Server. The audit completed 253 tests and produced a hardening index score
of 63. Several configuration warnings and hardening suggestions were identified, which
will be addressed during the remediation phase to improve the overall security posture
of the system.

### 2.2 Remediation Actions

<img width="862" height="140" alt="Screenshot 2025-12-22 081925" src="https://github.com/user-attachments/assets/8db0d3d9-57f8-4674-a5a4-c3cdbb346974" />

ClamAV was installed to provide host-based malware protection. Virus signature databases
were updated successfully using freshclam, ensuring the system maintains current threat
definitions.

<img width="560" height="71" alt="Screenshot 2025-12-22 082049" src="https://github.com/user-attachments/assets/af921c09-55f8-4f6f-9a3c-df06e631cb26" />

Automatic security updates were verified using unattended-upgrades to ensure that critical
security patches are applied regularly without manual intervention.

<img width="915" height="68" alt="Screenshot 2025-12-22 083745" src="https://github.com/user-attachments/assets/b0979f98-86ea-4328-857f-644a2e5ef49d" />

SSH configuration was verified to confirm that root login is disabled, password-based
authentication is disabled, and public key authentication is enforced. This reduces the
risk of brute-force and credential-based attacks.

<img width="498" height="188" alt="Screenshot 2025-12-22 083944" src="https://github.com/user-attachments/assets/6cb47a8e-cbd8-4357-ab54-490d7fe3a0b5" />

Firewall configuration was verified using UFW, confirming a default-deny policy for
incoming traffic with SSH explicitly permitted for remote administration. This limits
exposure to unnecessary network services.

### 2.3 Post-Remediation Lynis Scan

<img width="646" height="630" alt="Screenshot 2025-12-22 084641" src="https://github.com/user-attachments/assets/9692d1cf-0c67-4040-8a90-a1cfefe3e19c" />

Following the application of targeted security remediation actions, Lynis was re-run to
reassess the system security posture. The hardening index increased from 63 to 64,
confirming that the applied measures, including malware protection, SSH hardening, and
firewall verification, positively improved the system’s security baseline.


## 3. Network Security Assessment (nmap)

<img width="532" height="153" alt="Screenshot 2025-12-22 085026" src="https://github.com/user-attachments/assets/2dd587a9-fe1b-4dd5-8a79-25a61e522a44" />

A network security assessment was performed using nmap to identify exposed services on
the Ubuntu Server. The scan confirmed that only SSH (port 22) is accessible, with all
other ports closed, indicating a minimal external attack surface.

## 4. Access Control Verification

<img width="828" height="180" alt="Screenshot 2025-12-22 085812" src="https://github.com/user-attachments/assets/a368852e-4a57-4fc9-9554-fca427cb9548" />

Access control was verified to ensure administrative privileges are restricted to
authorised users. The system is accessed using a dedicated administrative account
(adminuser) with privilege escalation managed through sudo. Direct root login is
disabled, enforcing the principle of least privilege.


## 5. Service Audit and Justification

<img width="831" height="673" alt="Screenshot 2025-12-22 090019" src="https://github.com/user-attachments/assets/3b8c659d-6a6d-44f9-a0cd-0a48bbdb5836" />

A review of running services was conducted to identify active system components.
Essential services were observed, including ssh.service for secure remote
administration, ufw for firewall enforcement, and clamav-freshclam.service for malware
definition updates. Core systemd services and user session managers were also present
and are required for normal operating system functionality.

No unnecessary or externally exposed services were identified, indicating that the
system maintains a minimal and controlled service footprint.

## 6. System Configuration Review

A system configuration review was conducted to evaluate core security-related settings
on the Ubuntu Server. The operating system was confirmed to be a supported LTS release
with automatic security updates enabled. SSH configuration enforces key-based
authentication with root login and password authentication disabled. Firewall rules
restrict inbound traffic to SSH only, and access control is managed through a dedicated
administrative user with sudo privileges.

Overall, the system configuration aligns with security best practices for a headless
Linux server and supports a minimal, well-controlled attack surface.

## 7. Remaining Risk Assessment

Despite the application of targeted security hardening measures, some residual risks
remain. These include the possibility of zero-day vulnerabilities, delayed patch
availability, and configuration drift over time. As the system relies on remote access,
there is also an inherent risk associated with credential compromise, although this is
significantly reduced through key-based authentication and restricted access controls.

These risks are mitigated through the use of automatic security updates, minimal service
exposure, strong access control policies, and ongoing monitoring. Regular security
reviews and audits would further reduce long-term risk as the system evolves.

## 8. Final Reflection

## Final Reflection

This project provided practical experience in deploying, securing, monitoring, and
evaluating a Linux-based server environment using industry-standard tools and
methodologies. Across the weekly phases, the system evolved from a basic virtualised
installation into a hardened, monitored, and audited server suitable for remote
administration.

Key learning outcomes included the importance of layered security, the value of
key-based authentication over password-based access, and the role of automation in
maintaining system security through unattended updates. Performance testing highlighted
how different workloads impact CPU, memory, disk, and network resources, reinforcing the
need for monitoring before and during system stress.

The security audit phase demonstrated that system hardening is an iterative process
rather than a one-time task. Tools such as Lynis and nmap were effective in identifying
weaknesses, while remediation activities improved the overall security posture of the
system. The process also reinforced the necessity of justifying running services and
minimising the attack surface.

Overall, this coursework strengthened both technical and analytical skills and improved
confidence in managing Linux servers in a secure and structured manner. The experience
reflects real-world system administration practices and provides a solid foundation for
future work in server management and cybersecurity.





