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


## Skills Demonstrated

Linux administration, virtual machine deployment, SIEM installation, endpoint onboarding, log analysis, network troubleshooting, service management, and technical documentation.

## Disclaimer

This project is intended for educational purposes and uses a controlled home lab. Any security testing will be restricted to systems that I own or am explicitly authorized to test.
