# Week 2 – Security Planning and Testing Methodology

## 1. Performance Testing Plan and Monitoring Methodology

This section defines the performance testing approach that will be used later in the
coursework to evaluate system behaviour under different workloads. Performance testing
will be conducted remotely from the Linux Mint workstation using SSH-based monitoring
tools and scripts [1].

Key performance metrics [2] to be monitored include CPU usage, memory usage, disk activity,
and network utilisation. These metrics will be collected during baseline operation and
while test applications are running on the Ubuntu Server.

Monitoring will be performed using standard Linux command-line tools and custom scripts
executed remotely via SSH. This approach allows performance data to be collected without
direct interaction with the server console, reflecting professional remote
administration practices.

## 2. Security Configuration Checklist
This section outlines the security controls that will be implemented and verified in
later weeks of the coursework. These controls are selected based on identified risks
and best practice for securing Linux server environments.

- SSH hardening  
  - Disable password-based authentication  
  - Enforce key-based authentication  
  - Restrict SSH access to the workstation system  

- Firewall configuration  
  - Enable a host-based firewall  
  - Permit SSH access only from trusted sources  
  - Block all unnecessary inbound traffic  

- Mandatory access control  
  - Enable and configure AppArmor  
  - Verify enforced profiles for critical services  

- Automatic updates  
  - Enable unattended security updates  
  - Verify update status and logging  

- User privilege management  
  - Create a non-root administrative user  
  - Apply the principle of least privilege  

- Network security  
  - Limit exposed services  
  - Maintain isolated host-only networking where appropriate  

## 3. Threat Model and Mitigation Strategies

This threat model identifies key security threats relevant to the coursework system and
outlines planned mitigation strategies [3].

| Threat | Description | Planned Mitigation |
|------|------------|-------------------|
| Unauthorised SSH access | Weak authentication or exposed SSH service | SSH hardening, key-based authentication, firewall restrictions |
| Service misconfiguration | Incorrect network or service settings | Firewall rules, configuration review, access control |
| Privilege escalation | Excessive administrative permissions | Non-root user accounts, least privilege enforcement |
| Resource abuse | Excessive CPU or memory usage | Monitoring and performance testing |

### Week 2 Reflection

This week focused on planning security controls and defining a structured testing
methodology rather than immediately implementing configurations. By identifying
potential threats and risks first, it became clearer why specific security controls
such as SSH hardening, firewall rules, and privilege management are necessary.

Creating a performance testing plan alongside the security checklist helped establish
clear objectives for future monitoring and evaluation. This planning ensures that later
security implementations and performance tests are purposeful, measurable, and aligned
with identified risks rather than applied arbitrarily.

## References

[1]
“OpenSSH: Manual Pages,” www.openssh.com. https://www.openssh.com/manual.html

‌[2]
Ubuntu, “Security | Ubuntu,” Ubuntu, 2019. https://ubuntu.com/security

‌[3]
NIST, “Guide for conducting risk assessments,” Guide for Conducting Risk Assessments, vol. 1, Sep. 2012, doi: https://doi.org/10.6028/nist.sp.800-30r1

