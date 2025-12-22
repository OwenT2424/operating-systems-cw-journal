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
real-time and historical analysis of CPU, memory, disk I/O, and network performance [2], [3].
These tools will be used to establish baseline system metrics prior to stress testing.

## 3. Baseline System Information

### 3.1 CPU and Kernel Information

<img width="811" height="760" alt="Screenshot 2025-12-22 062615" src="https://github.com/user-attachments/assets/dd5d5f54-7f85-4e4e-982c-299085878a2f" />

CPU and kernel information was collected to document the system architecture and
processing capabilities under idle conditions. This establishes a baseline for
evaluating performance during later stress testing [3].

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

## 5. Mandatory Security Controls

### 5.1 Access Control Enforcement (AppArmor)

<img width="374" height="87" alt="Screenshot 2025-12-22 091345" src="https://github.com/user-attachments/assets/9b698891-d41c-4862-877a-8f9c29f4518c" />

Ubuntu Server uses AppArmor as its mandatory access control framework. AppArmor was
verified to be active and enforcing security profiles for system applications.

The AppArmor status output confirms that the kernel module is loaded, profiles are
installed, and multiple profiles are operating in enforce mode. Enforced profiles
restrict application capabilities and limit the potential impact of compromised
processes beyond traditional user and group permissions.

### 5.2 Automatic Security Updates

<img width="558" height="57" alt="Screenshot 2025-12-22 091637" src="https://github.com/user-attachments/assets/6a035b00-5357-4a3a-830c-0248580f99de" />

Automatic security updates were configured using unattended-upgrades to ensure that
critical patches are applied regularly without manual intervention. This reduces the
window of exposure to known vulnerabilities.

### 5.3 Intrusion Detection with fail2ban

<img width="182" height="128" alt="Screenshot 2025-12-22 092653" src="https://github.com/user-attachments/assets/acdb70d6-d673-4b03-9482-32a785e3acf3" />

<img width="1522" height="610" alt="Screenshot 2025-12-22 092805" src="https://github.com/user-attachments/assets/ca50f93b-decf-48b3-9a0f-c516aafb59af" />

Fail2Ban was installed and configured to provide intrusion detection and automated
response for the SSH service. A custom `jail.local` configuration was created to
enable the SSH daemon jail with defined retry limits and ban durations.

The SSH jail monitors authentication logs and temporarily bans IP addresses that
exceed the allowed number of failed login attempts. This reduces the risk of brute
force attacks against the SSH service.

Verification confirmed that the Fail2Ban service is active, enabled on system startup,
and that the SSH jail is running with no active bans under normal conditions.

## 6. Security Baseline Verification Script

A baseline verification script (`security-baseline.sh`) was created to automatically
validate security controls implemented in Phases 4 and 5. The script checks effective
SSH hardening settings, firewall status and rules, AppArmor enforcement status,
unattended-upgrades configuration, and Fail2Ban service/jail operation.

Automating baseline checks supports repeatable verification and helps detect
configuration drift over time.

```bash
#!/usr/bin/env bash
# security-baseline.sh
# Purpose: Verify security configurations implemented in Phases 4 and 5.

# Exit immediately if a command fails (helps catch misconfigurations quickly).
set -e

# Print a title banner for readability.
echo "=============================="
echo " Security Baseline Verification"
echo "=============================="
echo ""

# Show when the script was executed (useful for journaling and evidence).
echo "[INFO] Run time: $(date)"
echo ""

# ------------------------------
# 1) SSH Hardening Verification
# ------------------------------
echo "----- SSH Hardening -----"

# Check effective SSHD configuration and extract key settings we hardened.
# Using sudo because sshd -T needs access to host keys and full config.
SSH_EFFECTIVE="$(sudo sshd -T | grep -E '^(permitrootlogin|passwordauthentication|pubkeyauthentication) ')"

# Print the extracted SSH settings.
echo "$SSH_EFFECTIVE"
echo ""

# Validate key SSH hardening requirements:
# - Root login must be disabled
# - Password authentication must be disabled
# - Public key authentication must be enabled
echo "$SSH_EFFECTIVE" | grep -q "^permitrootlogin no" || { echo "[FAIL] SSH: permitrootlogin is not set to 'no'"; exit 1; }
echo "$SSH_EFFECTIVE" | grep -q "^passwordauthentication no" || { echo "[FAIL] SSH: passwordauthentication is not set to 'no'"; exit 1; }
echo "$SSH_EFFECTIVE" | grep -q "^pubkeyauthentication yes" || { echo "[FAIL] SSH: pubkeyauthentication is not set to 'yes'"; exit 1; }

# If all checks pass, report success.
echo "[PASS] SSH hardening verified."
echo ""

# ------------------------------
# 2) Firewall (UFW) Verification
# ------------------------------
echo "----- Firewall (UFW) -----"

# Capture verbose firewall status output.
UFW_STATUS="$(sudo ufw status verbose)"

# Print the firewall status (evidence for journal/video).
echo "$UFW_STATUS"
echo ""

# Validate firewall requirements:
# - Firewall must be active
# - Default inbound policy should be deny
# - SSH (22/tcp) should be allowed
echo "$UFW_STATUS" | grep -qi "Status: active" || { echo "[FAIL] UFW: firewall is not active"; exit 1; }
echo "$UFW_STATUS" | grep -qi "Default: deny (incoming)" || { echo "[WARN] UFW: default incoming policy is not clearly 'deny'"; }
echo "$UFW_STATUS" | grep -qE "22/tcp\s+ALLOW IN" || { echo "[FAIL] UFW: SSH (22/tcp) is not allowed"; exit 1; }

echo "[PASS] UFW firewall verified."
echo ""

# ------------------------------
# 3) Mandatory Access Control (AppArmor) Verification
# ------------------------------
echo "----- AppArmor (MAC) -----"

# Show AppArmor status to confirm the kernel module is loaded and profiles enforced.
# This is your Phase 5 access control requirement.
AA_STATUS="$(sudo aa-status)"

# Print the AppArmor status (evidence).
echo "$AA_STATUS"
echo ""

# Basic validations:
# - Module must be loaded
# - At least one profile should be in enforce mode
echo "$AA_STATUS" | grep -qi "apparmor module is loaded" || { echo "[FAIL] AppArmor: module not loaded"; exit 1; }
echo "$AA_STATUS" | grep -qi "profiles are in enforce mode" || { echo "[WARN] AppArmor: enforce mode not detected"; }

echo "[PASS] AppArmor status verified."
echo ""

# ------------------------------
# 4) Automatic Security Updates Verification
# ------------------------------
echo "----- Automatic Updates -----"

# Verify unattended-upgrades package is installed (Phase 5 requirement).
dpkg -s unattended-upgrades >/dev/null 2>&1 && echo "[PASS] unattended-upgrades package is installed." || { echo "[FAIL] unattended-upgrades not installed"; exit 1; }

# Display configuration file that enables periodic updates (evidence).
AUTO_UPGRADES_FILE="/etc/apt/apt.conf.d/20auto-upgrades"

# Print the configuration file contents if it exists.
if [[ -f "$AUTO_UPGRADES_FILE" ]]; then
  echo "[INFO] $AUTO_UPGRADES_FILE:"
  cat "$AUTO_UPGRADES_FILE"
else
  echo "[FAIL] $AUTO_UPGRADES_FILE not found"
  exit 1
fi

echo ""

# Check that periodic updates and unattended upgrades are enabled.
grep -q 'APT::Periodic::Update-Package-Lists "1";' "$AUTO_UPGRADES_FILE" || { echo "[FAIL] Auto updates: Update-Package-Lists not enabled"; exit 1; }
grep -q 'APT::Periodic::Unattended-Upgrade "1";' "$AUTO_UPGRADES_FILE" || { echo "[FAIL] Auto updates: Unattended-Upgrade not enabled"; exit 1; }

echo "[PASS] Automatic security updates verified."
echo ""

# ------------------------------
# 5) Intrusion Detection (fail2ban) Verification
# ------------------------------
echo "----- Fail2Ban -----"

# Check fail2ban service state.
F2B_ACTIVE="$(systemctl is-active fail2ban || true)"
F2B_ENABLED="$(systemctl is-enabled fail2ban || true)"

# Print service state results.
echo "[INFO] fail2ban active: $F2B_ACTIVE"
echo "[INFO] fail2ban enabled: $F2B_ENABLED"
echo ""

# Validate fail2ban is active.
[[ "$F2B_ACTIVE" == "active" ]] || { echo "[FAIL] Fail2Ban is not active"; exit 1; }

# Show fail2ban jail list (evidence).
sudo fail2ban-client status
echo ""

# Show SSH jail status (evidence that sshd jail is running).
sudo fail2ban-client status sshd
echo ""

echo "[PASS] Fail2Ban verified (service active and sshd jail present)."
echo ""

# ------------------------------
# 6) Malware Scanner (ClamAV) Verification (Optional but strong evidence)
# ------------------------------
echo "----- Malware Scanner (ClamAV) -----"

# Check that clamav-freshclam service exists and is active (signature updates).
CLAM_ACTIVE="$(systemctl is-active clamav-freshclam 2>/dev/null || true)"
echo "[INFO] clamav-freshclam active: $CLAM_ACTIVE"

# If service is present but inactive, warn rather than fail (some setups update manually).
if [[ "$CLAM_ACTIVE" == "active" ]]; then
  echo "[PASS] ClamAV update service is active."
else
  echo "[WARN] ClamAV update service not active (verify updates are applied)."
fi

echo ""
echo "=============================="
echo " Baseline verification complete"
echo "=============================="
```

<img width="474" height="598" alt="Screenshot 2025-12-22 100352" src="https://github.com/user-attachments/assets/9196d024-b7d8-4c6d-a963-ede7f76167ac" />
<img width="432" height="499" alt="Screenshot 2025-12-22 100323" src="https://github.com/user-attachments/assets/642e4c27-7893-4cb4-b25d-225b10ad7fd1" />

Below is the output of the AppArmor section, it wasn't included in the above screenshots for the sake of clarity.

```text
----- AppArmor (MAC) -----
apparmor module is loaded.
156 profiles are loaded.
59 profiles are in enforce mode.
   /snap/snapd/24792/usr/lib/snapd/snap-confine
   /snap/snapd/24792/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /snap/snapd/25577/usr/lib/snapd/snap-confine
   /snap/snapd/25577/usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/bin/evince
   /usr/bin/evince-previewer
   /usr/bin/evince-previewer//sanitized_helper
   /usr/bin/evince-thumbnailer
   /usr/bin/evince//sanitized_helper
   /usr/bin/evince//snap_browsers
   /usr/bin/freshclam
   /usr/bin/man
   /usr/lib/cups/backend/cups-pdf
   /usr/lib/snapd/snap-confine
   /usr/lib/snapd/snap-confine//mount-namespace-capture-helper
   /usr/sbin/clamd
   /usr/sbin/cups-browsed
   /usr/sbin/cupsd
   /usr/sbin/cupsd//third_party
   lsb_release
   man_filter
   man_groff
   nvidia_modprobe
   nvidia_modprobe//kmod
   plasmashell
   plasmashell//QtWebEngineProcess
   rsyslogd
   snap-update-ns.firefox
   snap-update-ns.firmware-updater
   snap-update-ns.snap-store
   snap-update-ns.snapd-desktop-integration
   snap.firefox.firefox
   snap.firefox.geckodriver
   snap.firefox.hook.configure
   snap.firefox.hook.disconnect-plug-host-hunspell
   snap.firefox.hook.install
   snap.firefox.hook.post-refresh
   snap.firmware-updater.firmware-notifier
   snap.firmware-updater.firmware-updater
   snap.firmware-updater.firmware-updater-app
   snap.firmware-updater.hook.configure
   snap.snap-store.hook.configure
   snap.snap-store.show-updates
   snap.snap-store.snap-store
   snap.snapd-desktop-integration.hook.configure
   snap.snapd-desktop-integration.snapd-desktop-integration
   tcpdump
   ubuntu_pro_apt_news
   ubuntu_pro_esm_cache
   ubuntu_pro_esm_cache//apt_methods
   ubuntu_pro_esm_cache//apt_methods_gpgv
   ubuntu_pro_esm_cache//cloud_id
   ubuntu_pro_esm_cache//dpkg
   ubuntu_pro_esm_cache//ps
   ubuntu_pro_esm_cache//ubuntu_distro_info
   ubuntu_pro_esm_cache_systemctl
   ubuntu_pro_esm_cache_systemd_detect_virt
   unix-chkpwd
   unprivileged_userns
5 profiles are in complain mode.
   /usr/sbin/sssd
   transmission-cli
   transmission-daemon
   transmission-gtk
   transmission-qt
0 profiles are in prompt mode.
0 profiles are in kill mode.
92 profiles are in unconfined mode.
   1password
   Discord
   MongoDB Compass
   QtWebEngineProcess
   balena-etcher
   brave
   buildah
   busybox
   cam
   ch-checkns
   ch-run
   chrome
   crun
   desktop-icons-ng
   devhelp
   element-desktop
   epiphany
   evolution
   firefox
   flatpak
   foliate
   geary
   github-desktop
   goldendict
   ipa_verify
   kchmviewer
   keybase
   lc-compliance
   libcamerify
   linux-sandbox
   loupe
   lxc-attach
   lxc-create
   lxc-destroy
   lxc-execute
   lxc-stop
   lxc-unshare
   lxc-usernsexec
   mmdebstrap
   msedge
   nautilus
   notepadqq
   obsidian
   opam
   opera
   pageedit
   podman
   polypane
   privacybrowser
   qcam
   qmapshack
   qutebrowser
   rootlesskit
   rpm
   rssguard
   runc
   sbuild
   sbuild-abort
   sbuild-adduser
   sbuild-apt
   sbuild-checkpackages
   sbuild-clean
   sbuild-createchroot
   sbuild-destroychroot
   sbuild-distupgrade
   sbuild-hold
   sbuild-shell
   sbuild-unhold
   sbuild-update
   sbuild-upgrade
   scide
   signal-desktop
   slack
   slirp4netns
   steam
   stress-ng
   surfshark
   systemd-coredump
   thunderbird
   toybox
   trinity
   tup
   tuxedo-control-center
   userbindmount
   uwsgi-core
   vdens
   virtiofsd
   vivaldi-bin
   vpnns
   vscode
   wike
   wpcom
12 processes have profiles defined.
11 processes are in enforce mode.
   /usr/bin/freshclam (66152) 
   /usr/sbin/cups-browsed (1455) 
   /usr/sbin/cupsd (1368) 
   /usr/lib/cups/notifier/dbus (1447) /usr/sbin/cupsd
   /usr/lib/cups/notifier/dbus (1453) /usr/sbin/cupsd
   /usr/lib/cups/notifier/dbus (1454) /usr/sbin/cupsd
   /usr/sbin/rsyslogd (945) rsyslogd
   /snap/snapd-desktop-integration/315/usr/bin/snapd-desktop-integration (5587) snap.snapd-desktop-integration.snapd-desktop-integration
   /snap/snapd-desktop-integration/315/usr/bin/snapd-desktop-integration (5674) snap.snapd-desktop-integration.snapd-desktop-integration
   /snap/snapd-desktop-integration/315/usr/bin/snapd-desktop-integration (9526) snap.snapd-desktop-integration.snapd-desktop-integration
   /snap/snapd-desktop-integration/315/usr/bin/snapd-desktop-integration (9666) snap.snapd-desktop-integration.snapd-desktop-integration
0 processes are in complain mode.
0 processes are in prompt mode.
0 processes are in kill mode.
1 processes are unconfined but have a profile defined.
   /usr/bin/gjs-console (15442) desktop-icons-ng
0 processes are in mixed mode.

[PASS] AppArmor status verified.
```

## 7. Remote Monitoring Script

A remote monitoring script (`monitor-server.sh`) was created on the Linux Mint
workstation to collect performance metrics from the Ubuntu Server via SSH. The script
performs a connectivity check and then gathers key performance indicators including
uptime/load averages, CPU summary, memory usage, disk utilisation, process snapshots,
and network interface information [1].

To support non-interactive execution, key-based authentication was configured and an
SSH host alias (`ubuntu-server`) was added in `~/.ssh/config`. This ensures the script
always uses the correct identity file and connects reliably without password prompts.

The script outputs results to the terminal for live monitoring and also saves a
timestamped log file for repeatable baseline evidence and later comparison during
stress testing.

```bash
#!/usr/bin/env bash
# monitor-server.sh
# Purpose: Remote monitoring script that runs on the workstation (Linux Mint),
#          connects to the Ubuntu Server via SSH, and collects key performance metrics.
# Requirement: Script must be commented line-by-line (done below).

# Exit immediately if any command fails (helps avoid silent errors).
set -e

# ---- Configuration ----
# Server SSH username (admin user created for administration).
SERVER_USER="adminuser"

# Server IP address on the host-only network.
SERVER_IP="192.168.56.102"

# Combine user and IP into a single SSH target string.
TARGET="ubuntu-server"

# Optional: output log file name (timestamped for evidence and repeatability).
OUTFILE="monitor-$(date +%Y-%m-%d_%H-%M-%S).log"

# ---- Helper output formatting ----
# Print a clear header line to make output readable in the terminal/video.
print_header() {
  echo "========================================"
  echo "$1"
  echo "========================================"
}

# Run a command remotely over SSH and label it.
run_remote() {
  local label="$1"     # A human-readable label for the command.
  local cmd="$2"       # The actual command to run on the server.

  print_header "$label"

  # -o BatchMode=yes avoids password prompts (requires key-based SSH to be configured).
  # -o ConnectTimeout=5 prevents hanging if the server is unreachable.
  ssh -o BatchMode=yes -o ConnectTimeout=5 "$TARGET" "$cmd"

  echo ""  # Blank line between sections for readability.
}

# ---- Start of monitoring run ----
# Record where and when the script ran from (useful for journaling).
print_header "Remote Monitoring Run (Workstation)"
echo "Workstation time: $(date)"
echo "Target server: $TARGET"
echo "Log file: $OUTFILE"
echo ""

# Write the same header into the log file.
{
  echo "Remote Monitoring Run"
  echo "Workstation time: $(date)"
  echo "Target server: $TARGET"
  echo ""
} > "$OUTFILE"

# ---- Connectivity check ----
# Confirm we can reach the server (SSH must be configured with keys).
print_header "Connectivity Check"
if ssh -o BatchMode=yes -o ConnectTimeout=5 "$TARGET" "echo 'SSH connection OK: ' \$(hostname)"; then
  echo "[PASS] SSH connectivity confirmed."
else
  echo "[FAIL] Cannot SSH into the server. Check IP, SSH service, and keys."
  exit 1
fi
echo ""

# ---- Collect key performance metrics ----
# 1) Uptime and load average (quick view of system activity).
run_remote "Uptime & Load Average" "uptime" | tee -a "$OUTFILE"

# 2) CPU details (useful once; shows cores and CPU model on the server).
run_remote "CPU Information (summary)" "lscpu | egrep 'Model name|CPU\\(s\\)|Thread\\(s\\) per core|Core\\(s\\) per socket|Socket\\(s\\)'" | tee -a "$OUTFILE"

# 3) Memory usage (human readable).
run_remote "Memory Usage" "free -h" | tee -a "$OUTFILE"

# 4) Disk usage (human readable).
run_remote "Disk Usage" "df -h" | tee -a "$OUTFILE"

# 5) Top processes by CPU (non-interactive snapshot).
#    head limits output to keep it readable.
run_remote "Top Processes (CPU snapshot)" "ps -eo pid,user,%cpu,%mem,cmd --sort=-%cpu | head -n 10" | tee -a "$OUTFILE"

# 6) Top processes by memory (non-interactive snapshot).
run_remote "Top Processes (Memory snapshot)" "ps -eo pid,user,%mem,%cpu,cmd --sort=-%mem | head -n 10" | tee -a "$OUTFILE"

# 7) Network interface summary and IP addresses (verify host-only interface).
run_remote "Network Interfaces & IPs" "ip -brief addr" | tee -a "$OUTFILE"

# 8) Quick network counters (RX/TX totals).
#    This is a lightweight way to show traffic changing over time.
run_remote "Network Counters (RX/TX bytes)" "cat /proc/net/dev | egrep 'lo:|enp|eth|ens'" | tee -a "$OUTFILE"

# ---- Completion message ----
print_header "Monitoring Complete"
echo "Saved log to: $OUTFILE"
echo "Done."
```

<img width="472" height="50" alt="Screenshot 2025-12-22 105947" src="https://github.com/user-attachments/assets/5d5018ae-c9cd-449d-8a70-6cc2f1a3ca01" />
<img width="722" height="101" alt="Screenshot 2025-12-22 104928" src="https://github.com/user-attachments/assets/8318848b-6363-48ed-bfda-ef46153b87d6" />

Key-based authentication was configured for automated monitoring by generating a
workstation SSH key pair and installing the public key on the server. A host alias was
then configured to ensure reliable non-interactive SSH connections for scripted monitoring.

<img width="1102" height="793" alt="Screenshot 2025-12-22 105134" src="https://github.com/user-attachments/assets/4812abbf-a6ef-4204-a2a1-fee4961f9bf4" />
<img width="665" height="809" alt="Screenshot 2025-12-22 105111" src="https://github.com/user-attachments/assets/eecea300-b7d5-4ccc-a191-f9b5b710a6e9" />
<img width="1047" height="319" alt="Screenshot 2025-12-22 105149" src="https://github.com/user-attachments/assets/0478b0fb-da2f-4b27-9e26-b80a866d1039" />


## 8. Baseline Performance Summary

Under idle conditions, the Ubuntu Server demonstrated low CPU utilisation, stable memory
usage, negligible disk I/O, and minimal network activity. These measurements establish a
baseline reference for evaluating system behaviour during stress testing in later weeks.

In addition to manual observation, baseline performance data can now be collected
remotely and repeatably using the `monitor-server.sh` script. This ensures consistent
baseline measurements over time and supports comparison against future stress-testing
results [3].

## 9. Week 5 Reflection

Week 5 focused on establishing both performance visibility and security assurance through
monitoring and automation. Baseline performance metrics were collected under idle
conditions to provide a reliable reference point for future stress testing and system
evaluation.

Beyond observation, this phase highlighted the importance of automation in system
administration. The creation of the `security-baseline.sh` script enabled repeatable
verification of security controls including SSH hardening, firewall configuration,
mandatory access control (AppArmor), automatic updates, malware scanning, and fail2ban.
This ensures configuration drift can be detected quickly.

The `monitor-server.sh` script demonstrated how remote monitoring can be performed
securely using SSH key-based authentication. Automating performance data collection
improves consistency, reduces manual error, and supports long-term system analysis.

Overall, this week reinforced the value of combining security controls with monitoring
and automation to create a maintainable, auditable, and resilient server environment.

## References

[1]
“The /proc Filesystem — The Linux Kernel documentation,” Kernel.org, 2024. https://www.kernel.org/doc/html/latest/filesystems/proc.html

[2]
“htop(1) - Linux manual page,” Man7.org, 2019. https://man7.org/linux/man-pages/man1/htop.1.html

[3]
“Sysstat Home Page,” Github.io, 2025. https://sysstat.github.io/

