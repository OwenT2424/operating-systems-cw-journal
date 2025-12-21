# Week 4 – Security Configuration and Hardening

## 1. SSH Hardening

<img width="1029" height="413" alt="Screenshot 2025-12-21 040856" src="https://github.com/user-attachments/assets/61efe1c0-356c-44e6-9083-355118dc286c" />

The SSH service was verified to be active and running on the Ubuntu Server. The service
was enabled to start automatically at boot and is listening on port 22, confirming that
secure remote access is available for administration.

<img width="813" height="41" alt="Screenshot 2025-12-21 041328" src="https://github.com/user-attachments/assets/37e799fb-cb8c-4e36-9691-0f488c3007ee" />

A backup of the SSH configuration file was created prior to applying any hardening
changes. This ensures the original configuration can be restored if required and
reduces the risk of accidental service disruption.

<img width="622" height="380" alt="Screenshot 2025-12-21 042855" src="https://github.com/user-attachments/assets/e5357ceb-e515-4d41-9fc7-1c46d624d69d" />

An SSH key pair was generated on the Linux Mint workstation using the ed25519 algorithm.
Key-based authentication provides stronger security than password-based access and is
used to secure remote administration of the Ubuntu Server.

<img width="942" height="266" alt="Screenshot 2025-12-21 043521" src="https://github.com/user-attachments/assets/fbfd53e9-e447-4f60-87fa-f0c95ad5a517" />

The workstation’s public SSH key was successfully copied to the Ubuntu Server using
ssh-copy-id. After verifying the server’s host fingerprint, key-based authentication
was enabled, allowing secure passwordless SSH access.

<img width="557" height="270" alt="Screenshot 2025-12-21 045805" src="https://github.com/user-attachments/assets/5aa6fda1-7988-4cfa-a6f4-eaef62d8aa8c" />

SSH access to the Ubuntu Server was successfully tested using key-based authentication.
The server was accessed without the use of a password, confirming that secure
passwordless authentication is functioning correctly.

<img width="635" height="70" alt="df3476fa-082d-4d85-ae9e-429e913f8239" src="https://github.com/user-attachments/assets/f9fa0af1-b9e8-4021-85dd-bbbf8f2489eb" />
<img width="313" height="192" alt="Screenshot 2025-12-21 051303" src="https://github.com/user-attachments/assets/0adf9a46-00d1-4935-ac90-d3b2e03d4b2c" />

The SSH configuration file was updated to disable root login and password-based
authentication while enforcing key-based authentication. These changes reduce the risk
of brute-force attacks and unauthorised access.

<img width="402" height="41" alt="Screenshot 2025-12-21 060554" src="https://github.com/user-attachments/assets/1487d8a4-76c2-4553-ab32-b4b97ba2b55a" />

The SSH configuration was tested using sshd -t to verify that no syntax errors were
present before restarting the service. This helps prevent accidental service failure
or administrator lockout.

<img width="998" height="460" alt="Screenshot 2025-12-21 061421" src="https://github.com/user-attachments/assets/70358234-dfbb-4e87-ad0c-140e00895e32" />

The SSH service was restarted after applying hardening changes and verified to be active
and running. This confirms that secure, key-based SSH access remains available following
configuration updates.


## 2. Firewall Configuration

<img width="642" height="343" alt="Screenshot 2025-12-21 061736" src="https://github.com/user-attachments/assets/55f40b7f-b79c-4a53-a996-685e8c83a5bc" />

The UFW firewall was enabled to restrict inbound traffic to the Ubuntu Server. SSH access
on port 22 was explicitly allowed to maintain secure remote administration, while all
other inbound connections are denied by default.


## 3. User and Privilege Management

<img width="921" height="544" alt="Screenshot 2025-12-21 062231" src="https://github.com/user-attachments/assets/c3218b6d-312a-4d97-8d36-b7be2672a886" />

A new administrative user account was created on the Ubuntu Server. Creating a separate
user account supports better access control and reduces reliance on the default user
for administrative tasks.

<img width="578" height="65" alt="Screenshot 2025-12-21 062914" src="https://github.com/user-attachments/assets/d1d65015-92bb-435e-a161-451b466b36c4" />

The newly created administrative user was added to the sudo group, granting controlled
administrative privileges. This approach supports the principle of least privilege by
separating standard user activity from administrative tasks.

## 4. Automatic Security Updates

<img width="681" height="84" alt="Screenshot 2025-12-21 063423" src="https://github.com/user-attachments/assets/714566c3-35bd-46e8-a4a9-461be7a6fb85" />

Automatic security updates were enabled using unattended-upgrades. The system is now
configured to automatically update package lists and apply security patches, reducing
the risk of exposure to known vulnerabilities.


Week 4 focused on implementing core security controls on the Ubuntu Server. Secure
remote access was established through SSH hardening, including the use of key-based
authentication and the removal of password-based access. A host-based firewall was
configured to restrict inbound network traffic while preserving secure administration.

User and privilege management was improved by creating a separate administrative
account with controlled sudo access, supporting the principle of least privilege.
Automatic security updates were also enabled to ensure that critical vulnerabilities
are patched without manual intervention.

These steps significantly reduced the system’s attack surface and aligned the server
configuration with industry-standard security practices. The week reinforced the
importance of applying changes incrementally and verifying system availability after
each configuration step.



