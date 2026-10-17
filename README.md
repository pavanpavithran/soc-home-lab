# Wazuh SOC Home Lab

## Overview

This project documents the deployment of a home Security Operations Center (SOC) lab using Wazuh. 

## Objectives

- Deploy a self-hosted Wazuh SIEM and security monitoring platform.
- Configure and enroll a Linux endpoint.
- Collect and analyze endpoint security telemetry.
- Investigate security alerts and understand Wazuh detection rules.
- Practice documenting findings and recommending remediation.

## Architecture

The lab currently consists of two virtual machines hosted on an Apple Silicon Mac using UTM.

| Component | Configuration |
|---|---|
| Host | Mac with Apple M3 chip |
| Hypervisor | UTM |
| SIEM server OS | Ubuntu Server 24.04.5 LTS |
| SIEM server resources | 4 CPU cores, 8 GB RAM, approximately 96 GB disk |
| SIEM platform | Wazuh all-in-one deployment |
| Wazuh version | Version 4.14.9 |
| Endpoint OS | Ubuntu Server 24.04.5 LTS |
| Endpoint agent | Wazuh Agent 4.14.9 |
| Networking | UTM shared networking |

### Components

- **Wazuh Manager:** Receives and analyzes endpoint security events.
- **Wazuh Indexer:** Stores and indexes security data.
- **Wazuh Dashboard:** Provides an interface for monitoring and investigating alerts.
- **Ubuntu Endpoint:** Generates telemetry collected by the Wazuh agent.

## Deployment

### 1. Virtual Machine Preparation

Created an Ubuntu Server VM in UTM and allocated CPU, memory, and disk resources.

The root filesystem initially occupied approximately 48.5 GB despite the virtual disk being approximately 100 GB. Inspected the LVM layout and expanded the root logical volume and filesystem.

Verified the final filesystem allocation using:

```bash
df -h /
```

### 2. Wazuh Server Installation

Updated Ubuntu packages and deployed the Wazuh all-in-one installation using the official installation assistant.

The installation completed successfully, and the generated dashboard administrator credentials were saved securely.

### 3. Dashboard Access and Verification

Accessed the dashboard from the Mac using HTTPS and the server's VM IP address.

Validated the dashboard locally using:

```bash
curl -k -I https://localhost
```

Received an HTTP 302 redirect to the login page, confirming that the dashboard was responding.

Also tested connectivity from the Mac to the VM.

### 4. Ubuntu Endpoint Deployment

Created a second Ubuntu VM in UTM and verified network connectivity to the Wazuh server.

Installed Wazuh Agent 4.14.9 and started the agent service.

### 5. Troubleshooting Agent Enrollment

**Issue:** The agent service was running, but the endpoint did not appear in the Wazuh dashboard.

**Investigation:** Examined the agent service status and `/var/ossec/logs/ossec.log`.

The logs showed repeated enrollment failures:

```text
Unable to connect to enrollment service at '[192.168.64.28]:1515'
```

**Root cause:** The agent was configured to contact an incorrect Wazuh server IP address. The actual server address was `192.168.64.27`.

**Resolution:** Corrected the server address in the agent configuration and restarted the agent service.

**Outcome:** Agent enrollment succeeded.

## Validation

- [x] Wazuh server and dashboard installed.
- [x] Dashboard accessible from the Mac.
- [x] Ubuntu endpoint created.
- [x] Wazuh agent installed and running.
- [x] Agent enrollment issue identified and resolved.
- [x] Confirm endpoint status is Active in the dashboard.
- [x] Verify endpoint telemetry is being received.
- [ ] Generate and investigate test security alerts.

## Future Work

- Configure and test File Integrity Monitoring (FIM).
- Investigate failed SSH login events.
- Analyze Linux authentication logs.
- Explore Wazuh detection rules and alert severity.
- Document a simulated security incident.
- Add a Kali Linux VM for controlled attack simulations against the lab endpoint.

## Skills Demonstrated

Linux administration, virtual machine deployment, SIEM installation, endpoint onboarding, log analysis, network troubleshooting, service management, and technical documentation.

## Disclaimer

This project is intended for educational purposes and uses a controlled home lab. Any security testing will be restricted to systems that I own or am explicitly authorized to test.
