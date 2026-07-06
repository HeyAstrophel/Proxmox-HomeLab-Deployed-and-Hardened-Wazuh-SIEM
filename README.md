# Proxmox-HomeLab-Deployed-and-Hardened-Wazuh-SIEM
A virtualized home lab environment deployed on dedicated mini-PC hardware using a Proxmox hypervisor to host an enterprise-level SIEM stack. This project focuses on the end-to-end installation, defensive configuration, and security hardening of the central platform, establishing a baseline infrastructure for scalable endpoint monitoring."

# Multi-Node SIEM & XDR Lab Deployment (Wazuh & Proxmox)

An enterprise-grade Security Operations Center (SOC) home lab environment built to simulate real-world endpoint monitoring, log analysis, and threat detection. This project demonstrates the complete lifecycle of a SIEM deployment—from virtualized infrastructure provisioning to system hardening and endpoint onboarding.
## 🛠️ System Architecture & Topology

The deployment is hosted within a dedicated Type-1 hypervisor environment, isolating security monitoring infrastructure from production traffic.

* **Hypervisor:** Proxmox VE
* **Compute Hardware:** Lenovo ThinkCentre (Ryzen 7, 32GB RAM)
* **Host Operating System:** Ubuntu Server 24.04 LTS (Minimal installation selected to minimize the initial attack surface and eliminate unnecessary background packages)

> [!NOTE]
> **Hypervisor Initialization:** Post-installation, the Proxmox host was optimized using an automated VE post-install configuration script. This run disabled the enterprise subscription nag, enabled the stable community pve-no-subscription repositories, and verified baseline microcode updates to ensure hypervisor stability before spinning up the security monitoring nodes.

### Resource Allocation
| Component | vCPU | RAM | Storage | Purpose |
| :--- | :---: | :---: | :---: | :--- |
| **Wazuh Manager** | 4 | 8 GiB | 50 GB | Centralized SIEM, Indexer, & Dashboard |

---

## 🚀 Milestone 1: Central Server Deployment

1. **Base OS Installation:** Provisioned a clean Ubuntu Server instance on Proxmox. Configured static networking and restricted initial packages to minimize the attack surface.
2. **Remote Access:** Configured secure OpenSSH access to pivot from the hypervisor console to a localized terminal.
3. **SIEM Stack Provisioning:** Deployed the unified Wazuh stack (Indexer, Server, and Dashboard) using the official automated installation assistant to ensure proper cryptographic certificate generation between internal API components.

```bash
curl -sO [https://packages.wazuh.com/4.14/wazuh-install.sh](https://packages.wazuh.com/4.14/wazuh-install.sh) && sudo bash ./wazuh-install.sh -a
